---
description: >-
  This document outlines how to implement Stacks based authentication to your
  React app.
---

# Authentication

The foundation of any Stacks based application is authentication. You are able to add authentication to any react application. Stacks auth is dependent on your users having a compatible wallet to authenticate through. Currently, the Hiro Web Wallet is the only wallet that is supported.&#x20;

Before adding authentication, make sure you've properly set up your application to work with `micro-stacks`.

### useAuth

The primary way you'll implement authentication is via the `useAuth` hook. This hook exposes a few callbacks for different functions (`handleSignIn`, `handleSignIn`), along with some helper variables: `isLoading` `isSignedIn`. Check out the sample below for a very simple `WalletConnectButton` component:

```typescript
import { useAuth } from "@micro-stacks/react";

export const WalletConnectButton = () => {
  const { isSignedIn, handleSignIn, handleSignOut, isLoading } = useAuth();
  return (
    <button onClick={isSignedIn ? handleSignOut : handleSignIn}>
      {isLoading
        ? "Loading..."
        : isSignedIn
        ? "Sign out"
        : "Connect Stacks Wallet"}
    </button>
  );
};
```

{% hint style="info" %}
`micro-stacks` has built-in support for cross-tab communication! This means if your user has two windows open of your application, their sessions will sync automatically.
{% endhint %}

#### Auth response payload

handleSignIn returns a payload of type `StacksSessionState`

```typescript
interface StacksSessionState {
    addresses: {
        testnet: string;
        mainnet: string;
    };
    appPrivateKey: string;
    associationToken: string;
    hubUrl: string;
    public_keys?: string[];
    profile: Profile;
    profile_url: string;
    username: string | null;
    version?: string;
    decentralizedID: string;
    identityAddress?: string;
}
```

And with that, once a user authenticates, your application will have their session saved until they sign out.

When there is an active user session, you are now able to display account-specific user data. Feel free to continue to the next page to learn more about what user data is available to you.

{% content-ref url="user-data.md" %}
[user-data.md](user-data.md)
{% endcontent-ref %}