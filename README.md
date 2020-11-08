# useGoogleMapsScript

This hook can be used to load the Google Maps API script as a hook. It is heavily based on a hook provided by [@react-google-maps/api](https://github.com/JustFly1984/react-google-maps-api), but can be used when you don't need the rest of Google Maps provided by this library.

```tsx
import { ReactNode } from 'react';
import { useGoogleMapsScript, Libraries } from 'use-google-maps-script';

export function App() {
  return (
    <LoadScript googleMapsApiKey={process.env.NEXT_PUBLIC_GOOGLE_API_KEY}>
      <SearchBox />
    </LoadScript>
  );
}

interface LoadScriptProps {
  googleMapsApiKey: string;
  children: ReactNode;
}

// Important to either declare outside component or memoize to avoid re-renders
const libraries: Libraries = ['places'];

function LoadScript({ googleMapsApiKey, children }: LoadScriptProps) {
  const { isLoaded, loadError } = useLoadScript({
    googleMapsApiKey,
    libraries,
  });

  if (!isLoaded) return <div>Loading script</div>;
  if (loadError) return <div>Error loading script</div>;
  return children;
}

function SearchBox() {
  // Could be used with https://use-places-autocomplete.netlify.app/
  return <div>Search Box which relies on google maps script.</div>;
}
```
