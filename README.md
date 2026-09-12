# Flowery

<div align="center">

### Flower E-Commerce Application

A modern flower e-commerce application built with Flutter, providing users with a complete shopping experience from discovering flowers and occasions to checkout, payment, and real-time order tracking.

</div>

---

## 📱 Overview

**Flowery** is a flower e-commerce application designed to provide a smooth and personalized shopping experience.

The application allows users to explore flowers and different occasions, manage their cart, complete checkout and payment, and track their orders in real time.

One of the main engineering aspects of the project is the **flexible payment architecture**, implemented using the **Strategy Design Pattern**, alongside a real-time delivery tracking system using Google Maps and live driver location updates.

> **Note:** Flowery is a team project. The sections below highlight the features and engineering work I personally contributed to.

---

## ✨ Key Features

* 🌸 Flower browsing and discovery
* 🎁 Occasion-based flower collections
* 🔎 Product discovery
* 🛒 Shopping cart
* 🧾 Checkout flow
* 💳 Multiple payment methods
* 🧩 Strategy Design Pattern for payment
* 📦 Order management
* 🚚 Order status tracking
* 🗺️ Real-time delivery tracking
* 📍 Live driver location
* 🗺️ Custom Google Maps styling
* 🚗 Vehicle-specific driver markers
* 👤 User profile
* 🔐 Authentication
* 🌍 Localization
* 📱 Responsive mobile UI

---

## 🌸 E-Commerce Experience

Flowery provides users with a complete flower shopping experience.

Users can explore available flowers, browse products based on different occasions, add items to their cart, and proceed through a dedicated checkout flow.

The application focuses on keeping the shopping experience simple while providing clear product information and an easy path from product discovery to order placement.

### Shopping Flow

```text
Browse Flowers
      │
      ▼
Select Product
      │
      ▼
Add to Cart
      │
      ▼
Review Cart
      │
      ▼
Checkout
      │
      ▼
Payment
      │
      ▼
Order Created
```

---

## 🛒 Cart & Checkout

The checkout flow brings together the main components required to complete an order.

The process includes:

* Reviewing cart items
* Managing quantities
* Reviewing order details
* Selecting a payment method
* Processing payment
* Creating the order
* Tracking the order after checkout

The checkout implementation was structured to keep payment-specific logic separated from the main checkout flow.

---

## 💳 Payment System

One of the main engineering contributions in Flowery was designing the payment system using the **Strategy Design Pattern**.

Instead of coupling the checkout logic to a specific payment implementation, payment methods are represented as interchangeable strategies.

### Payment Architecture

```text
                    Checkout
                       │
                       ▼
                PaymentRepository
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
        Payment A   Payment B   Payment C
```

This allows the application to switch between different payment methods without changing the core checkout logic.

### Why Strategy Pattern?

The Strategy Pattern allows each payment method to encapsulate its own behavior while exposing a common abstraction to the checkout feature.

This provides:

* Easier addition of new payment methods
* Reduced coupling
* Better separation of responsibilities
* Easier testing
* Cleaner checkout logic

The design also follows the **Dependency Inversion Principle**, since the higher-level checkout logic depends on an abstraction rather than concrete payment implementations.

### Implementation Structure

```text
Checkout Feature
│
├── Presentation
│   └── CheckoutCubit
│
├── Domain
│   └── PaymentRepository
│
└── Data
    └── Repositories
        ├── PaymentImplementationA
        ├── PaymentImplementationB
        └── PaymentImplementationC
```

---

## 📦 Order Tracking

After placing an order, users can track the progress of their delivery.

The tracking experience provides information about the current order status and allows users to follow the delivery process.

### Order Tracking Flow

```text
Order Placed
     │
     ▼
Order Confirmed
     │
     ▼
Preparing Order
     │
     ▼
Out for Delivery
     │
     ▼
Delivered
```

The order status is reflected in the application as the delivery progresses.

---

## 🗺️ Real-Time Delivery Tracking

One of the key features I worked on was the real-time delivery tracking system.

The driver's location is continuously streamed and displayed on a Google Maps interface inside the customer application.

### Live Tracking Architecture

```text
Driver App
    │
    │ Live Location Stream
    ▼
Firebase
    │
    │ Location Updates
    ▼
Customer App
    │
    ▼
Google Maps
    │
    ▼
Driver Marker
```

Instead of periodically requesting the driver's location, the application listens to a live stream of location updates.

This allows the driver's position on the map to update as the driver moves.

---

## 📍 Live Driver Location

The tracking system listens for changes in the driver's location and updates the map accordingly.

The flow can be summarized as:

```text
Location Update
      │
      ▼
Location Stream
      │
      ▼
State Update
      │
      ▼
Update Driver Position
      │
      ▼
Google Maps Marker
```

This provides a more responsive tracking experience while avoiding unnecessary manual polling.

---

## 🗺️ Custom Google Maps

The Google Maps interface was customized to match the application's visual identity.

Custom map styling was applied instead of relying entirely on the default Google Maps appearance.

The customized map includes:

* Custom map theme
* Custom map styling
* Customized driver marker
* Driver location updates
* Map camera movement

<!-- Add Google Maps screenshot here -->

---

## 🚗 Vehicle-Specific Driver Markers

The driver marker changes depending on the vehicle being used for the delivery.

For example:

```text
Vehicle Type
     │
     ├── 🚗 Sedan
     │      └── Sedan Marker
     │
     ├── 🚐 Van
     │      └── Van Marker
     │
     ├── 🛵 Scooter
     │      └── Scooter Marker
     │
     └── 🏍️ Motorcycle
            └── Motorcycle Marker
```

This provides users with more contextual information about their delivery driver directly on the map.

<!-- Add vehicle marker screenshots here -->

---

## 🧠 State Management

The application uses **BLoC/Cubit** for state management.

Cubits are responsible for coordinating UI state and feature logic while keeping widgets focused primarily on presentation.

For example, the checkout flow separates UI state from payment implementation details.

```text
UI
 │
 ▼
CheckoutCubit
 │
 ▼
PaymentRepository
 │
 ├── Payment Strategy A
 ├── Payment Strategy B
 └── Payment Strategy C
```

The same separation is applied to the delivery tracking flow.

```text
Google Maps UI
      │
      ▼
Tracking Cubit
      │
      ▼
Location Stream
      │
      ▼
Firebase
```

---

## 🏗️ Architecture

The project follows a **Clean Architecture** approach with a feature-oriented structure.

The main goal is to separate responsibilities between presentation, business logic, and infrastructure.

### High-Level Structure

```text
lib/
│
├── core/
│   ├── ...
│
└── features/
    ├── auth/
    ├── home/
    ├── products/
    ├── cart/
    ├── check_out/
    ├── orders/
    ├── profile/
    └── ...
```

The application separates responsibilities across:

```text
Presentation
     │
     ▼
Domain
     │
     ▼
Data
```

This keeps feature logic independent from infrastructure-specific implementations.

---

## 🧩 Dependency Injection

Dependency injection is used to keep dependencies explicit and reduce coupling between application layers.

The project uses:

* `GetIt`
* `Injectable`

This allows services and repositories to be registered centrally and injected where required.

For example, payment implementations can be provided to the checkout feature without tightly coupling the checkout logic to a specific implementation.

---

## 🛠️ Tech Stack

| Technology             | Usage                                  |
| ---------------------- | -------------------------------------- |
| **Flutter**            | Cross-platform mobile application      |
| **Dart**               | Application development                |
| **BLoC / Cubit**       | State management                       |
| **Firebase**           | Backend services                       |
| **Firebase Firestore** | Data persistence and real-time updates |
| **Google Maps**        | Maps and delivery tracking             |
| **GetIt**              | Dependency injection                   |
| **Injectable**         | Dependency registration                |
| **Clean Architecture** | Application architecture               |
| **Git**                | Version control                        |
| **Figma**              | UI/UX design                           |

---

## 👨‍💻 My Contribution

As part of the development team, I was responsible for several major areas of the application.

### 🛒 Checkout & Payment

* Implemented checkout flow
* Designed payment abstraction
* Implemented multiple payment strategies
* Applied Strategy Design Pattern
* Applied Dependency Inversion Principle
* Integrated payment implementations with CheckoutCubit

### 🗺️ Order Tracking

* Implemented order tracking experience
* Integrated Google Maps
* Implemented real-time driver location tracking
* Connected location streams to the application state
* Updated driver position on the map
* Implemented custom Google Maps styling

### 🚗 Driver Tracking

* Implemented custom driver markers
* Added vehicle-specific markers
* Supported different delivery vehicle types
* Updated markers based on driver's vehicle

### Additional Work

* BLoC/Cubit state management
* Firebase integration
* Dependency injection
* UI implementation
* Feature integration
* Performance and UI behavior improvements

---

## 🎯 Engineering Focus

While building Flowery, I focused not only on implementing the required screens but also on keeping the application maintainable and extensible.

Some of the engineering considerations included:

* Using the Strategy Pattern to make payment methods interchangeable
* Applying Dependency Inversion to reduce coupling
* Separating payment logic from checkout logic
* Using streams for real-time driver location updates
* Keeping UI state separate from infrastructure-specific services
* Customizing Google Maps to match the application design
* Using dynamic driver markers based on vehicle type
* Structuring features around Clean Architecture principles
* Using dependency injection to manage application dependencies

---

## 🎨 Design

The application's UI/UX was designed in Figma and translated into reusable Flutter components.

The design includes dedicated flows for:

* Onboarding
* Authentication
* Home
* Product discovery
* Product details
* Cart
* Checkout
* Payment
* Order tracking
* Delivery tracking
* Profile

<!-- Add UI / Figma screenshots here -->

---

## 📸 Screenshots

### 🏠 Home & Product Discovery

| Home                    | Home Loading            |
| ----------------------- | ----------------------- |
| <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-48-55-455_com example elevate_flower_app" src="https://github.com/user-attachments/assets/14ab854d-94c0-4a4d-a753-a054f6e19bc6" />          | <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-48-43-800_com example elevate_flower_app" src="https://github.com/user-attachments/assets/34093ebb-bcfd-4785-9da5-4b2653917ed8" /> |

---

### 🛒 Cart & Checkout

| Cart                    | Checkout                |
| ----------------------- | ----------------------- |
| <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-51-54-337_com example elevate_flower_app" src="https://github.com/user-attachments/assets/80de84a7-a7c1-4f46-a198-243a24455141" />     | <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-52-01-131_com example elevate_flower_app" src="https://github.com/user-attachments/assets/bfe11114-c262-4a7f-96fc-fbef3249beea" /> | 
|                         | <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-52-09-188_com example elevate_flower_app" src="https://github.com/user-attachments/assets/fbb8eaab-3369-4ec8-94a1-a4f722fd9f7d" /> |

---

### 💳 Payment

| Payment Method          | Payment Result |
| ----------------------- | -------------- |
| <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-52-01-131_com example elevate_flower_app" src="https://github.com/user-attachments/assets/a213002d-5531-46e4-b291-50ab90d452a7" />          |  <img width="1080" height="2400" alt="Screenshot_2026-09-12-00-53-12-432_com example elevate_flower_app" src="https://github.com/user-attachments/assets/d459ace2-2fdb-45d1-a89a-e0f111de3d08" />|

