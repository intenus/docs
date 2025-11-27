---
description: API References
icon: send-backward
---

# Intent Classification API

Intent Classification API — core service of _Intenus_ that classifies user intents and generates scoring strategies using ML models

{% hint style="info" %}
For details on strategy ranking, refer to the related documentation [ranking-strategies.md](../../core-concepts/ranking-strategies.md "mention")
{% endhint %}

{% openapi-operation spec="API" path="/predict" method="post" %}
[OpenAPI API](http://3.26.14.143:8000/openapi.json)
{% endopenapi-operation %}

{% openapi-schemas spec="API" schemas="AssetType,HTTPValidationError,Intent,OptimizationGoal,PredictionResponse,TimeInForce,ValidationError" grouped="true" %}
[OpenAPI API](http://3.26.14.143:8000/openapi.json)
{% endopenapi-schemas %}
