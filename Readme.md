# firestore-pagination-hook

Cumulative pagination for firestore collections

## Install

```
yarn add firestore-pagination-hook
```

## Example

```jsx
import usePagination from "firestore-pagination-hook";
import firebase from "firebase/app";

function Example() {
  const {
    loading,
    loadingError,
    loadingMore,
    loadingMoreError,
    hasMore,
    items,
    loadMore
  } = usePagination(
    firebase
      .firestore()
      .collection("recipes")
      .where("userId", "==", 1)
      .orderBy("updatedAt", "desc"),
    {
      limit: 25
    }
  );

  return (
    <div>
      {loading && <div>Loading...</div>}
      {items.map(item => (
        <div>{item.id}</div>
      ))}
      {hasMore && !loadingMore && <button onClick={loadMore}>Load more</button>}
    </div>
  );
}
```
