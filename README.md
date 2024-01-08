<center>

# ProductiVue

![ProductiVue](./public/ProductiVue.webp)

Minimalistic Peripheral View for my Productivity Sessions

![Vue.js Badge](https://img.shields.io/badge/Vue.js-4FC08D?logo=vuedotjs&logoColor=fff&style=for-the-badge)
![Tauri Badge](https://img.shields.io/badge/Tauri-24C8D8?logo=tauri&logoColor=fff&style=for-the-badge)
![TypeScript Badge](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=fff&style=for-the-badge)
![Rust Badge](https://img.shields.io/badge/Rust-000?logo=rust&logoColor=fff&style=for-the-badge)

</center>

## About

My goals for ProductiVue are:

- To provide a customizable, minimalistic view on my second monitor
- To be able to view chat from YouTube Live and Twitch stream in one source
- To practice my Vue, Typescript and Rust skills

## Setup

Download via git:

```
git clone https://github.com/liyunze-coding/ProductiVue.git
```

If you do not have pnpm:

```
npm install -g pnpm
```

Install via pnpm:

```
pnpm install
```

Start with Tauri (web and desktop app view):

```
pnpm run tauri dev
```

Or web view only

```
pnpm run dev
```

Build and get installer.exe in `src-tauri/target/release/bundle/nsis/ProductiVue_x.x.x_x64-setup.exe`:

```
pnpm run tauri build
```

## Notes

Can be compiled to work on the web, Windows, macOS and Linux.

