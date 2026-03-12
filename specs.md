# Pet Health Centre

> Ref URL: https://pethealthcentre.vn

## General

### Who Uses This?

- **Guest** – Unregistered users who want to browse centre info, products, and services
- **Customer** – Pet owners with a registered account
- **Staff** – Centre employees who manage appointments and inventory
- **Vet** – Veterinarians who view and update pet medical records

### What Is the Problem?

- Customers must call to book services — time-consuming and prone to scheduling errors
- Physical vet notebooks are easily lost and information is not stored centrally

### Why Is This Useful?

- Pet information and medical records are stored digitally, preventing data loss
- Customers can book services online without calling
- Staff and vets manage schedules and records directly on the platform

---

## Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Frontend   | TBD (React / Next.js recommended) |
| Backend    | Go                                |
| Database   | TBD (PostgreSQL recommended)      |
| Realtime   | WebSocket (future phase)          |
| Auth       | JWT                               |
| Deployment | TBD                               |

---

## Specifications

### Roles

| Role     | Description |
|----------|-------------|
| Guest    | Not logged in; can view public information |
| Customer | Registered; manages pets and books services |
| Staff    | Manages appointments, products, and customer chat |
| Vet      | Views and updates pet medical records |

---

### User Stories

#### Guest
- I want to view centre information (address, opening hours, contact) so I can decide if it suits my needs
- I want to browse and compare products so I can find the right one for my pet
- I want to view services and their details so I can decide whether to book
- I want to chat with staff directly on the website so I don't need to open another app

#### Customer
- I want to register and log in so I can access personalised features
- I want to create, view, edit, and delete my pet profiles so I don't have to re-enter details every time I book
- I want to book spa or vet services online so I don't have to call
- I want to view my booking and order history
- I want to add products to my cart and check out (mock payment) for a convenient shopping experience

#### Staff
- I want to view the daily and weekly appointment schedule so I know what needs to be done
- I want to confirm or cancel customer appointments to manage the schedule efficiently
- I want to chat with customers to give advice and support
- I want to check current product stock levels so I know when to reorder

#### Vet
- I want to view the day's appointment schedule so I can prepare in advance
- I want to view a pet's medical history so I can avoid prescribing medicines with adverse interactions
- I want to create and update medical records after each visit so history is stored digitally

---

## Features

### Must Have (MVP)

**Pet**
- CRUD pet profile (name, species, breed, age, photo)
- View list of pets linked to an account

**User / Auth**
- Register, log in, log out (JWT)
- CRUD user profile
- View booking and order history

**Product**
- Browse and search products
- View product details

**Service**
- View service list (spa, check-up, vaccination, etc.)
- Book a service for a pet

**Shopping**
- Add / remove products from cart
- Checkout (mock payment)

**Staff**
- View appointment schedule
- Confirm / cancel appointments

**Vet**
- View appointment schedule
- View, create, and update pet medical records

### Should Have (Phase 2)

- Product filter (by type, price, pet)
- Real payment gateway (VNPay / Momo)
- Realtime chat (Staff ↔ Customer)
- Notification system (email / in-app)
- Blog / knowledge articles
- Mobile app

### Nice to Have (Future)

- Delivery system
- Improved UI/UX & design system
- Analytics dashboard for Staff / Admin

---

## Success Metrics

- [ ] Guest can browse products and services without logging in
- [ ] Customer can register → add a pet → book a service end-to-end
- [ ] Customer can add products to cart → complete checkout (mock payment)
- [ ] Staff can view, confirm, and cancel appointments
- [ ] Vet can view and update a pet's medical record
- [ ] Staff can view current product stock quantity

---

## Open Questions

- Frontend framework: React / Next.js or Vue / Nuxt.js?
- Database: PostgreSQL or MySQL?
- Deployment: self-managed VPS or cloud (GCP / AWS)?
- Payment: VNPay or Momo integration for Phase 2?
- Admin role: is a separate Admin role needed to manage Staff and Vet accounts?
