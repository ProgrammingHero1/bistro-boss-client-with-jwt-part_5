# Bistro Boss Client with JWT

Welcome to the Bistro Boss Client with JWT repository. Today we added user authentication using JWT (JSON Web Tokens), allowing users to securely log in, sign up, and manage their sessions and worked on dashboard

[Server Repo Link](https://github.com/ProgrammingHero1/bistro-boss-server-with-jwt-part_5)

## New Packages Used

No new packages were used today.

## What We Did Today

- **Save User Data to Server:** Implemented functionality to save user data to the server upon registration and login.
- **Google Sign-In and When to Save User Info:** Added Google Sign-In integration and ensured user information is saved appropriately.
- **Save User if They Don’t Exist in the Database:** Ensured that user information is saved only if the user does not already exist in the database.
- **Load All Users on the Dashboard Page:** Implemented a feature to load and display all users on the dashboard.
- **Display All Users and Create Make Admin API:** Created an interface to display all users and an API to assign admin roles to users.
- **Make User Admin and Install JWT:** Implemented functionality to assign admin roles to users and integrated JWT for secure authentication.
- **Create a JWT Token and Save It in Local Storage:** Generated JWT tokens upon user login and stored them in local storage for session management.
- **Verify Token and Axios Interceptor:** Verified JWT tokens and set up Axios interceptors to manage API requests.
- **Logout Unauthorized Access and Check Is Admin:** Ensured unauthorized users are logged out and implemented admin role verification.
- **Make User API Secure Using Verify Admin:** Enhanced security by verifying admin roles for sensitive API endpoints.

## Important Code for Today

### useEffect for Auth State Management
```js
useEffect(() => {
    const unsubscribe = onAuthStateChanged(auth, currentUser => {
        setUser(currentUser);
        if (currentUser) {
            // Get token and store on client
            const userInfo = { email: currentUser.email };
            axiosPublic.post('/jwt', userInfo)
                .then(res => {
                    if (res.data.token) {
                        localStorage.setItem('access-token', res.data.token);
                    }
                });
        } else {
            // Remove token if user is logged out
            localStorage.removeItem('access-token');
        }
        setLoading(false);
    });
    return () => {
        return unsubscribe();
    };
}, [axiosPublic]);

```
