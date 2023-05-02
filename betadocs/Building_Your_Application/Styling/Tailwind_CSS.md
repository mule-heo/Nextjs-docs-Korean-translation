원본 링크: [https://beta.nextjs.org/docs/styling/tailwind-css](https://beta.nextjs.org/docs/styling/tailwind-css)

# \***\*Tailwind CSS\*\***

[Tailwind CSS](https://tailwindcss.com/)는 유틸리티  기반의 CSS 프레임워크로, Next.js와 매우 잘 작동합니다.

### **테일윈드 설치 (Installing Tailwind)**

Tailwind CSS 패키지를 설치하고 init 명령어를 실행하여 tailwind.config.js 및 postcss.confing.js 파일을 모두 생성합니다:

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

## \***\*테일윈드 구성 (Configuring Tailwind)\*\***

tailwind.config.js 내부에서 Tailwind CSS 클래스 이름을 사용할 파일들의 경로를 추가하세요:

```jsx
tailwind.config.js;

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}", // Note the addition of the `app` directory.
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",

    // Or if using `src` directory:
    "./src/**/*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

postcss.config.js를 수정할 필요는 없습니다.

## \***\*스타일 가져오기 (Importing Styles)\*\***

Tailwind에서 생성된 스타일을 삽입하기 위해 [Tailwind CSS directives](https://tailwindcss.com/docs/functions-and-directives#directives)(지시어)를 애플리케이션의 전역 스타일시트에 추가합니다. 예를 들어:

```css
app/globals.css

@tailwind base;
@tailwind components;
@tailwind utilities;
```

루트 레이아웃(app/layout.tsx) 내에서 globals.css 스타일시트를 가져와 애플리케이션의 모든 경로에 스타일을 적용합니다.

```jsx
app / layout.tsx;

// These styles apply to every route in the application
import "./globals.css";

export const metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode,
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

## \***\*클래스 사용 (Using Classes)\*\***

Tailwind CSS를 설치하고 전역 스타일을 추가한 후, 애플리케이션에서 Tailwind의 유틸리티 클래스를 사용할 수 있습니다.

```jsx
app / page.tsx;

export default function Page() {
  return <h1 className="text-3xl font-bold underline">Hello, Next.js!</h1>;
}
```

## \***\*Turbopack과 함께 사용 (Usage with Turbopack)\*\***

Next.js 13.1 부터 [Turbopack](https://turbo.build/pack/docs/features/css#tailwind-css)에서 Tailwind CSS 및 PostCSS가 지원됩니다.