# Bistro Boss Client with Cart

Welcome to the Bistro Boss Server repository. This project includes a cart system that allows users to add food items, view them in a dashboard, and update the cart dynamically.
[server Repo Link](https://github.com/ProgrammingHero1/bistro-boss-server-with-cart-part_4)
## New Packages Used

### @tanstack/react-query
- **Description:** @tanstack/react-query is a powerful data-fetching library for React applications. It simplifies server state management by providing hooks for fetching, caching, synchronizing, and updating server state in your React components. With built-in support for background refetching, caching, and more, it enhances the developer experience and improves application performance.

## What We Did Today

- **Developed Cart System for Added Food:** Implemented a cart system to allow users to add food items to their cart.
- **Created Dashboard for Showing the Cart Items:** Developed a dashboard interface where users can view the items in their cart.
- **Created Custom Hook Using @tanstack/react-query:** Built a custom hook using @tanstack/react-query to fetch and manage cart data.
- **Refetch Cart Data for Any Update of Cart Item:** Ensured that the cart data is refetched and updated dynamically upon any changes to the cart items.

## Important Code for Today

### useCart Hook
```js
import { useQuery } from "@tanstack/react-query";
import useAxiosSecure from "./useAxiosSecure";
import useAuth from "./useAuth";

const useCart = () => {
    const axiosSecure = useAxiosSecure();
    const { user } = useAuth();
    const { refetch, data: cart = [] } = useQuery({
        queryKey: ['cart', user?.email],
        queryFn: async() => {
            const res = await axiosSecure.get(`/carts?email=${user.email}`);
            return res.data;
        }
    });

    return [cart, refetch];
};

export default useCart;
```
