/* 

----------------------------------------------

Twirl by Jimmyhogs

----------------------------------------------

KFLOAT0 = Twirl Degree

KFLOAT1 = Twirl Angle

----------------------------------------------

KFLOAT0: 0 to 10; KFLOAT1: -360 to 360

----------------------------------------------

*/

float width  = (float)p_Width;
float height = (float)p_Height;


float2 center = (float2)(width * 0.5f, height * 0.5f);
float2 pos = (float2)((float)x, (float)y);
float2 delta = pos - center;

float targetAspect = 16.0f / 9.0f;
float actualAspect = width / fmax(height, 0.001f);

float2 aspectScale;

if (actualAspect > targetAspect) {
    aspectScale = (float2)(1.0f, actualAspect / targetAspect);
} else {
    aspectScale = (float2)(targetAspect / actualAspect, 1.0f);
}

float2 scaledDelta = delta * aspectScale;

float radius = length(scaledDelta);
float baseRadius = length(center * aspectScale);

float effectiveRadius = fmax(baseRadius, 0.001f);


float r = clamp(radius / effectiveRadius, 0.0f, 1.0f);

float soften = clamp(kFloat0, -10.0f, 10.0f);
float falloffPower = 1.0f;

if (soften > 0.0f) {
    falloffPower = fmax(soften, 1.0f);
}

float falloff = pow(fmax(1.0f - r, 0.0f), falloffPower);
falloff *= (r < 1.0f) ? 1.0f : 0.0f;

float strength = -kFloat1 * 0.01745329252f;
float angle = strength * falloff;

float s = sin(angle);
float c = cos(angle);

float2 rotated = (float2)(
    scaledDelta.x * c - scaledDelta.y * s,
    scaledDelta.x * s + scaledDelta.y * c
);

float2 samplePos = center + rotated / aspectScale;

if (samplePos.x < 0.0f ||
    samplePos.y < 0.0f ||
    samplePos.x >= width ||
    samplePos.y >= height) {
    kOutput = (float4)(0.0f);
} else {
    kReadIndex = samplePos;
    kRead();
}
