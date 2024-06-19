https://tailwindcss.com/docs/installation

1.

npm init

2.

npm i -D tailwindcss

3.

npx tailwindcss init

4.

module.exports =
content: ['./*.html'],

5.

@tailwind base;
@tailwind components;
@tailwind utilities;

6.

"scripts": {
"build": "tailwindcss -i ./input.css -o ./css/style.css",
"watch": "tailwindcss -i ./input.css -o ./css/style.css --watch"
},

7.

npm run build

8.

npm run watch

---

介紹 layer

@layer base {
h1 {
@apply text-3xl;
}

h2 {
font-size: 1.5rem;
}
}

介紹 components

@layer components {
.btn-blue {
@apply bg-blue-500 py-2 px-4 rounded-xl font-bold hover:bg-blue-700 text-white;
}
}

介紹 theme 函式

.content-area {
@apply bg-green-200
height: theme('spacing.128');
}

@media screen(xl) {
body {
@apply bg-black text-white;
}
}

---
