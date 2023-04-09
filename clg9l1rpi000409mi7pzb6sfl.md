---
title: "My Struggles with Red Squiggly Lines"
datePublished: Sun Apr 09 2023 15:51:53 GMT+0000 (Coordinated Universal Time)
cuid: clg9l1rpi000409mi7pzb6sfl
slug: my-struggles-with-red-squiggly-lines
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681055312657/b9f8609f-2b43-45e4-be18-c5aa90e1f9ed.png
tags: error, errors, programming-tips

---

# Introduction

As a developer, I've experienced the frustration that comes with encountering coding errors. This article, which I'll continuously update, serves as an error journal, documenting every programming error I've encountered and how I resolved it, regardless of its severity.

## Entry 1

While working on [Intergalactic Encyclopedia](https://github.com/Jemeni11/intergalactic-encyclopedia), I wanted to create a context to store the data I got from querying the [SWAPI.dev API](https://swapi.dev/).

In my \`api-data-context.ts\` file, I did this:

```typescript
import { createContext } from "react";

const defaultValue = {
  films: [],
  people: [],
  planets: [],
  species: [],
  starships: [],
  vehicles: [],
};

const ApiDataContext = createContext(defaultValue);

function ApiDataContextProvider(props: { children: React.ReactNode }) {
  return (
    <ApiDataContext.Provider value={defaultValue}>
      {props.children}
    </ApiDataContext.Provider>
  );
}
```

And I got this error:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1680620424364/4cbee6dc-0b3b-430f-9a9f-e027113cf30b.png align="center")

On a whim, I decided to get rid of the types I passed in as an argument to the `ApiDataContextProvider` function and change the extension of my file from `ts` to `js`. This surprisingly solved my problem but it seemed like a cop-out. I wanted to use TypeScript, not JavaScript.

If you have used TypeScript before you might have already seen the solution to my problem in the last paragraph. To end this, the proper file extension should have been `tsx` not `ts` . Apparently, `ts` and `tsx` cannot be used interchangeably the same way you use `js` and `jsx`.