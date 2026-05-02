# E-Shop

A full-stack e-commerce web application built with React and Redux Toolkit, featuring a customer-facing storefront and a protected admin dashboard with complete product, order, and user management.

---

## Features

### Customer
- Browse and filter products by gender, category, size, color, brand, material, and price
- Product detail pages with image gallery, size/color picker, and quantity selector
- Shopping cart synced with the backend and persisted in localStorage
- Stripe-powered checkout with shipping address form
- Order history and detailed order tracking

### Admin
- Protected dashboard accessible to admin users only
- Create, edit, and delete products with image upload
- View and update order delivery status
- Create, update roles for, and delete users

---

## The Process

The app is built around a standard React + Redux Toolkit architecture.

**Auth** is handled with JWT tokens stored in localStorage. On login or register, the token and user info are saved and loaded back on refresh. The `ProtectedRoutes` component guards any route that requires a logged-in user or a specific role.

**State** is split across dedicated Redux slices — one each for auth, cart, products, checkout, orders, and the three admin resources. Each slice owns its own async thunks via `createAsyncThunk` and handles loading and error states independently.

**Cart** is fetched from the backend on login and kept in sync on every add, update, or remove action. A copy is also saved to localStorage so the UI can reflect the cart immediately on page load without waiting for an API call.

**Checkout** works by sending cart and shipping data to the backend, which creates a Stripe session and returns a redirect URL. The frontend sends the user directly to Stripe's hosted payment page. On return, the success page hits the backend to verify the session and display the confirmed order.

**Routing** uses React Router v6 with nested layouts — a `UserLayout` wrapping all customer pages (with header and footer), and a separate `AdminLayout` with a collapsible sidebar for the dashboard.

---

## Running the Project

### Prerequisites
- Node.js 18+
- A running backend API

### 1. Clone the repo and install dependencies

```bash
git clone <repo-url>
cd e-shop-frontend
npm install
```

### 2. Set up environment variables

Create a `.env` file in the root of the project:

```env
VITE_API_URL=http://localhost:5000/api
```

### 3. Start the development server

```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

### 4. Build for production

```bash
npm run build
```
