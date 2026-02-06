## Product Choice

Yandex Taxi (Russian: Яндекс Такси, romanized: Yandeks Taksi; stylised as Yandex.Taxi), a division of Yandex, operates a ridesharing company in Russia, Moldova, Armenia, Azerbaijan, Belarus, Georgia, Kyrgyzstan, Serbia, Uzbekistan, Kazakhstan, Tajikistan, Israel and UAE. The Yandex Taxi division also operates Yandex Eda, a food delivery service; Yandex.Lavka, a grocery delivery service;and Yandex.Chef, previously known as Partiya Edy (Russian: "Food Party"), a meal kit service. All services are accessible via the Yandex Go mobile app. <https://taxi.yandex.ru>

## Main components

![Yandex.Go Component Diagram](./diagrams/out/yandex-go/architecture-component/Component%20Diagram.svg)
[Yandex.Go Component Diagram code](./diagrams/src/yandex-go/architecture-component.puml)

Notification Service - sends notification to device. \
Dispatch Service - connect taxi driver with user.\
Payment Service - provides payment.\
Maps & Routing Service - finds a route. \
Pricing Service - changes price.

## Data flow

![Yandex.Go Sequence Diagram](./diagrams/out/yandex-go/architecture-sequence/Sequence%20Diagram.svg)
[Yandex.Go Sequence Diagram code](./diagrams/src/yandex-go/architecture-sequence.puml)

**Group: 2. Price Estimation (Pre-Ride)**

In this flow, the user enters a destination in the mobile app, and a ride price is calculated before booking.
The Mobile App sends a request through the API Gateway to the Maps & Pricing service with pickup and drop-off coordinates.
The service fetches route and traffic data from the external Maps API, applies tariff rules, and checks demand surge.
Finally, available ride options (for example, Economy and Comfort) with estimated prices are returned to the mobile app.

## Deployment

![Yandex.Go Deployment Diagram](./diagrams/out/yandex-go/architecture-deployment/Deployment%20Diagram.svg)
[Yandex.Go Deployment Diagram code](./diagrams/src/yandex-go/architecture-deployment.puml)

## Assumptions

* I assume the **Maps & Pricing service** is responsible for calculating the final ride price, including surge pricing based on current demand and traffic conditions.
* I assume the **Dispatch service** performs driver matching internally using geospatial data and business rules, rather than delegating this logic to another microservice.

## Open questions

* How does the system handle **driver rejections or timeouts** during the matching process, and how many retries are allowed before the order is canceled?
* What **load balancing and scaling strategy** is used between microservices?
