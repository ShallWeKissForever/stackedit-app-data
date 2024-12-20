


> Written with [StackEdit中文版](https://stackedit.cn/).

# 目录

要达到能够胜任工作需求的 Next.js 技能水平，需要掌握以下几个关键知识点和技能，涵盖基本功能、进阶概念以及生产环境的最佳实践：

----------

### **1. 基础知识**

-   **React 基础**  
    确保熟悉 React，包括组件、状态管理（useState、useReducer 等）、生命周期（useEffect）以及 props 和 context。
    
-   **Next.js 基本概念**
    
    -   [页面路由（基于文件系统的路由）](#页面路由（基于文件系统的路由）是什么？)
    -   [API 路由（创建后端 API）](#什么是API路由？)
    -   [静态生成 (Static Site Generation, SSG)](#什么是静态生成？) 和[服务器端渲染 (Server Side Rendering, SSR)](#什么是服务器端渲染？)
    -   动态路由和动态页面渲染

----------

### **2. 核心功能**

-   **数据获取**  
    学习 `getStaticProps`、`getStaticPaths` 和 `getServerSideProps` 的用法，以及如何选择适合的渲染模式。
    
-   **页面导航**  
    使用 `next/link` 和 `useRouter` 实现页面跳转和动态导航。
    
-   **样式与设计**
    
    -   使用 CSS 模块、全局样式、Tailwind CSS 或 styled-components 等工具。
    -   掌握如何在 Next.js 项目中优化样式加载。
-   **API 路由**  
    编写简单的后端接口，用于处理数据请求和业务逻辑。
    
-   **图片优化**  
    学习 Next.js 的 `next/image` 组件，用于自动优化图片的加载和显示。
    
-   **国际化支持 (i18n)**  
    配置和实现多语言支持。
    

----------

### **3. 进阶功能**

-   **动态导入**  
    使用 `next/dynamic` 实现组件的按需加载，优化性能。
    
-   **中间件**  
    利用 Edge Functions 和中间件实现访问控制、请求重定向等功能。
    
-   **认证与授权**  
    实现用户登录、注册和访问控制，集成如 NextAuth.js 或 Firebase。
    
-   **API 集成**  
    掌握如何与 RESTful API 或 GraphQL API 交互（如通过 axios 或 Apollo Client）。
    
-   **性能优化**
    
    -   使用 Lazy Loading 和 Code Splitting。
    -   配置 Webpack 和 Next.js 的内置优化选项。
    -   了解如何分析和提升页面的加载速度（Lighthouse 或 Next.js Performance Insights）。
-   **部署与运维**
    
    -   使用 Vercel 部署 Next.js 项目。
    -   学习如何在其他平台（如 AWS、Docker 或自建服务器）上部署。
    -   配置 CDN 缓存、HTTPS 和 SEO。

----------

### **4. 项目实践**

通过项目练习，综合运用所学知识，以下是一些实用项目示例：

1.  **博客系统**  
    包含文章的 SSG、评论的 SSR、以及用户认证。
    
2.  **电商平台**  
    商品展示、购物车管理、支付集成（如 Stripe）和动态路由。
    
3.  **管理后台系统**  
    数据表格、动态表单、权限管理（基于 JWT 或 OAuth）。
    

----------

### **5. 工作场景需要的其他知识**

-   **前端工程化**
    
    -   熟悉 TypeScript，特别是类型定义和接口设计。
    -   使用 ESLint 和 Prettier 进行代码规范化。
    -   掌握 Git 工作流。
-   **团队协作技能**
    
    -   阅读和理解他人代码。
    -   在团队中参与代码评审。
    -   编写清晰的文档。
-   **了解相关生态**
    
    -   了解 UI 框架（如 Ant Design 或 Material UI）的集成方法。
    -   使用 Zustand 或 Redux 管理全局状态。

----------

通过学习上述内容，并结合实践项目，你可以达到在工作中使用 Next.js 的水平，能够高效地开发并优化现代化的 Web 应用程序。

----------
# 知识点

### **页面路由（基于文件系统的路由）是什么？** 

页面路由是 Next.js 的核心功能之一，它基于文件系统来定义前端页面的路由。每个文件或文件夹在 `pages` 或 `app` 目录下都会自动映射为一个前端路由，无需手动配置路由规则。

----------

### **如何使用页面路由？**

#### **Pages Router**

页面文件存放在 `pages` 目录下：

1.  创建静态页面：
    
    ```plaintext
    pages/
      index.js       ->   /
      about.js       ->   /about
      contact.js     ->   /contact
    ```
    
2.  动态路由： 文件名以方括号表示动态参数：
    
    ```plaintext
    pages/
      blog/
        [id].js      ->   /blog/:id
    ```
    
    示例代码：
    
    ```javascript
    // pages/blog/[id].js
    export default function BlogPost({ query }) {
      const { id } = query;
      return <h1>Blog Post {id}</h1>;
    }
    ```
    
3.  嵌套路由： 通过文件夹实现嵌套路径：
    
    ```plaintext
    pages/
      products/
        [category]/
          [id].js    ->   /products/:category/:id
    ```
    

#### **App Router**

页面文件存放在 `app` 目录下：

1.  路由文件格式为 `page.js` 或 `page.tsx`：
    
    ```plaintext
    app/
      about/
        page.js      ->   /about
      blog/
        [id]/
          page.js    ->   /blog/:id
    ```
    
2.  嵌套布局支持：
    
    ```plaintext
    app/
      layout.js       // 全局布局
      about/
        layout.js     // /about 专属布局
        page.js       // 页面
    ```
    

----------

### **解决了什么问题？**

1.  **简化路由配置**：
    
    -   不需要像传统框架（如 React Router）中手动定义每个路由。
    -   避免复杂的路由配置文件。
2.  **代码与路由一致性**：
    
    -   文件系统和路由结构保持同步，开发更直观。
3.  **动态路由简化**：
    
    -   动态参数通过文件名即可实现，无需额外配置解析逻辑。
4.  **嵌套路由问题**：
    
    -   通过目录结构实现嵌套路由，代码组织更清晰。
5.  **自动优化**：
    
    -   Next.js 自动处理路由优先级、懒加载等逻辑。

----------

### **有没有替代方案？**

1.  **React Router**：
    
    -   手动定义路由表，例如：
        
        ```javascript
        import { BrowserRouter, Route, Routes } from 'react-router-dom';
        
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route path="/blog/:id" element={<BlogPost />} />
          </Routes>
        </BrowserRouter>
        ```
        
2.  **Vue Router**（对于 Vue.js 项目）：
    
    -   Vue Router 提供手动配置和文件系统路由的功能。
3.  **手动实现路由**：
    
    -   使用 `window.location` 或 `history.pushState` 自行管理路由逻辑。
4.  **基于框架的路由工具**：
    
    -   如 Nuxt.js（用于 Vue）和 Remix（用于 React）。

----------

### **基于文件系统路由的好处**

1.  **开发效率高**：
    
    -   文件名即路由，无需额外配置。
2.  **可维护性强**：
    
    -   项目规模扩大时，文件系统天然帮助组织路由结构。
3.  **动态和嵌套路由易用**：
    
    -   动态路由和嵌套路由通过目录即可实现，逻辑直观。
4.  **与服务端功能集成**：
    
    -   Next.js 文件系统路由可以无缝支持 API 路由和 SSR（服务器端渲染）。

----------

### **使用场景**

1.  **单页应用（SPA）**：
    
    -   实现简单的导航和页面切换。
2.  **多页应用（MPA）**：
    
    -   每个路由加载独立的页面资源。
3.  **SEO 优化**：
    
    -   使用服务器渲染或静态生成生成优化的页面路径。
4.  **全栈开发**：
    
    -   前后端集成（如通过 `/pages/api` 实现后端逻辑）。

----------

### **工作原理**

1.  **文件扫描**：
    
    -   在构建时，Next.js 会扫描 `pages` 或 `app` 目录，根据文件和文件夹结构生成路由表。
2.  **路径映射**：
    
    -   文件路径映射到对应的 URL 路径，例如 `pages/about.js` 映射到 `/about`。
3.  **动态参数解析**：
    
    -   使用动态路由时，Next.js 会解析 URL 中的动态部分并注入到组件的 `props` 或 `query` 对象中。
4.  **懒加载**：
    
    -   每个路由页面会被打包为独立的文件，按需加载，提高性能。
5.  **优先级处理**：
    
    -   Next.js 根据路由定义顺序和文件路径自动处理优先级，无需手动干预。

----------

### **总结**

基于文件系统的页面路由是 Next.js 的一大特点，它通过简化路由配置、提升开发效率、增强代码可读性，成为现代全栈开发中的重要工具。适用于快速开发、SEO 优化和动态路由需求，尤其适合全栈和前后端一体化的项目。

[返回目录](#%E7%9B%AE%E5%BD%95)

### **什么是静态生成？**

静态生成 (Static Site Generation, SSG)是 Next.js 提供的一种预渲染方式，在**构建时**生成 HTML 文件。生成的静态页面在用户访问时直接提供，不需要再运行服务器逻辑，因而具有更快的加载速度和更好的性能。

SSG 是现代 Jamstack 架构的核心，适合内容相对静态、不需要频繁更新的页面。

----------

### **怎么用 SSG？**

在 Next.js 中，使用 `getStaticProps` 或 `getStaticPaths` 实现静态生成。

#### **1. 基础用法：`getStaticProps`**

`getStaticProps` 是一个运行在构建时的函数，用于获取页面的静态数据。

```javascript
// pages/blog/[id].js
export async function getStaticProps(context) {
  const { id } = context.params;
  const res = await fetch(`https://api.example.com/blog/${id}`);
  const post = await res.json();

  return {
    props: { post }, // 作为页面组件的 props
  };
}

export default function BlogPost({ post }) {
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}
```

#### **2. 动态路由：`getStaticPaths`**

当页面使用动态路由时，需要通过 `getStaticPaths` 指定需要生成的路径。

```javascript
export async function getStaticPaths() {
  const res = await fetch('https://api.example.com/blog');
  const posts = await res.json();

  const paths = posts.map((post) => ({
    params: { id: post.id.toString() },
  }));

  return { paths, fallback: false }; // fallback 控制未定义路径的处理
}
```

#### **结合使用**

```javascript
export async function getStaticProps({ params }) {
  const res = await fetch(`https://api.example.com/blog/${params.id}`);
  const post = await res.json();

  return { props: { post } };
}

export async function getStaticPaths() {
  const res = await fetch('https://api.example.com/blog');
  const posts = await res.json();

  const paths = posts.map((post) => ({
    params: { id: post.id.toString() },
  }));

  return { paths, fallback: false };
}
```

----------

### **解决了什么问题？**

1.  **提升性能：**
    
    -   通过构建时生成静态 HTML 文件，用户无需等待服务器生成页面，大大缩短响应时间。
2.  **SEO 优化：**
    
    -   由于页面在构建时生成完整 HTML 文件，搜索引擎可以直接抓取内容。
3.  **减少服务器负载：**
    
    -   静态文件由 CDN 分发，减少了对服务器的依赖，适合高流量的场景。
4.  **快速交付：**
    
    -   HTML 文件直接部署到 CDN，无需复杂的后端配置。

----------

### **有没有替代方案？**

1.  **服务器端渲染 (Server-Side Rendering, SSR)**：
    
    -   在每次请求时动态生成页面。
    -   适用于需要实时数据的场景。
    -   使用 `getServerSideProps`。
2.  **客户端渲染 (Client-Side Rendering, CSR)**：
    
    -   页面初始加载是空的，通过 JavaScript 动态获取数据并渲染。
    -   适用于需要交互性强或不需要 SEO 优化的场景。
3.  **增量静态生成 (Incremental Static Regeneration, ISR)**：
    
    -   是 SSG 的增强版，允许部分页面在后台增量更新，支持更灵活的动态内容。
    -   通过设置 `revalidate`。

----------

### **好处是什么？**

1.  **性能高：**
    
    -   静态文件由 CDN 提供，访问速度极快。
2.  **安全性强：**
    
    -   没有运行服务器端逻辑，减少潜在的安全风险。
3.  **易于扩展：**
    
    -   静态页面可以轻松扩展至全球，通过 CDN 提供服务。
4.  **开发简单：**
    
    -   开发者专注于页面内容，不必管理复杂的后端服务。

----------

### **使用场景是什么？**

1.  **博客和文档：**
    
    -   内容不频繁变化，适合静态生成以提升加载速度。
2.  **营销网站：**
    
    -   静态生成的页面可以快速交付并优化 SEO。
3.  **电商产品页面：**
    
    -   固定的产品详情页，适合使用 SSG 提高性能。
4.  **活动页面或展示页面：**
    
    -   内容固定的活动宣传或作品展示网站。

----------

### **原理是什么？**

1.  **构建时生成静态 HTML 文件**：
    
    -   Next.js 在构建时执行 `getStaticProps` 和 `getStaticPaths` 获取数据，并生成对应的 HTML 文件。
2.  **部署静态文件**：
    
    -   构建后的静态文件（HTML、CSS、JS 等）被部署到 CDN 或静态服务器。
3.  **请求时直接返回静态内容**：
    
    -   用户请求时，CDN 直接提供生成好的 HTML 页面，加载速度非常快。
4.  **结合增量更新**：
    
    -   如果启用增量静态生成（ISR），Next.js 会在后台重新生成更新的页面，同时不会影响用户的访问。

----------

### **总结**

静态生成（SSG）是一种高效的页面渲染方式，适合内容静态或更新频率较低的场景。结合增量静态生成（ISR），SSG 可以在保证性能的同时，支持动态更新需求。对于需要快速交付、提升 SEO 和性能的应用，SSG 是一种非常合适的选择。

[返回目录](#%E7%9B%AE%E5%BD%95)

### **什么是服务器端渲染？**

服务器端渲染 (Server Side Rendering, SSR) 是一种页面渲染方式。在 SSR 中，每次用户请求时，服务器会动态生成完整的 HTML 页面并发送到客户端。SSR 可以提高页面的首屏加载速度，并有助于搜索引擎优化（SEO）。

在 Next.js 中，SSR 是通过 `getServerSideProps` 方法实现的，它会在每次请求时运行，用于获取数据并渲染页面。

----------

### **怎么用 SSR？**

在 Next.js 中，可以通过以下方式实现 SSR：

#### **1. 使用 `getServerSideProps`**

`getServerSideProps` 是 Next.js 提供的一个函数，用于在每次请求时动态获取页面所需的数据。

```javascript
// pages/blog/[id].js
export async function getServerSideProps(context) {
  const { id } = context.params;
  const res = await fetch(`https://api.example.com/blog/${id}`);
  const post = await res.json();

  return {
    props: { post }, // 将数据传递给页面组件
  };
}

export default function BlogPost({ post }) {
  return (
    <article>
      <h1>{post.title}</h1>
      <p>{post.content}</p>
    </article>
  );
}
```

#### **2. 特点**

-   `getServerSideProps` 会在每次请求时执行，返回的数据直接作为页面的 `props`。
-   页面在服务端完成渲染后，将 HTML 返回给浏览器。

----------

### **解决了什么问题？**

1.  **动态数据实时性：**
    
    -   SSR 可以在每次请求时动态获取数据，适合需要频繁更新或依赖用户输入的场景。
2.  **SEO 优化：**
    
    -   搜索引擎可以直接抓取完整的 HTML 页面，而不需要等待 JavaScript 加载和执行。
3.  **首次加载性能：**
    
    -   页面在服务器上已经渲染完成，浏览器接收到的 HTML 是完整的，减少了首屏渲染时间。
4.  **统一的渲染环境：**
    
    -   数据获取逻辑在服务端运行，可以避免客户端与服务端数据不一致的问题。

----------

### **有没有替代方案？**

1.  **静态生成 (Static Site Generation, SSG)：**
    
    -   页面在构建时生成静态 HTML 文件。
    -   优点：性能更高，适合内容不频繁变化的场景。
    -   缺点：无法实时更新数据。
2.  **客户端渲染 (Client-Side Rendering, CSR)：**
    
    -   页面初始加载是空的，通过 JavaScript 在客户端获取数据并渲染页面。
    -   优点：无需服务器支持，动态交互性强。
    -   缺点：SEO 较差，首屏渲染时间较长。
3.  **增量静态生成 (Incremental Static Regeneration, ISR)：**
    
    -   在 SSG 基础上支持动态更新，允许后台重新生成部分页面。
    -   优点：性能接近 SSG，同时支持动态数据。

----------

### **好处是什么？**

1.  **实时数据支持：**
    
    -   每次请求都会获取最新数据，适合需要实时更新的页面。
2.  **更好的 SEO：**
    
    -   搜索引擎可以直接抓取完整的 HTML 页面内容，无需等待 JavaScript 执行。
3.  **首屏渲染快：**
    
    -   用户收到的是完整的 HTML 页面，无需等待客户端渲染。
4.  **灵活性高：**
    
    -   适合处理个性化内容、用户权限控制等需要动态生成页面的场景。

----------

### **使用场景是什么？**

1.  **电商网站：**
    
    -   商品详情页、购物车等需要实时展示最新库存和价格。
2.  **个性化内容：**
    
    -   用户主页、推荐内容等需要根据用户身份动态生成。
3.  **数据频繁更新的页面：**
    
    -   新闻网站、社交媒体、动态数据仪表盘。
4.  **SEO 要求高的动态页面：**
    
    -   营销页面、文章页面。

----------

### **原理是什么？**

1.  **客户端请求：**
    
    -   当用户请求页面时，浏览器向服务器发送 HTTP 请求。
2.  **服务端处理：**
    
    -   服务器执行 `getServerSideProps`，获取页面所需的数据。
    -   将数据与 React 组件结合，生成完整的 HTML。
3.  **返回 HTML：**
    
    -   服务器将生成的 HTML 页面返回给浏览器。
4.  **客户端接管：**
    
    -   页面加载后，React 在客户端启动，将页面变为可交互。

----------

### **SSR 的缺点**

1.  **服务器性能开销大：**
    
    -   每次请求都需要动态生成页面，对服务器资源消耗较大。
2.  **页面加载延迟：**
    
    -   相比 SSG，SSR 会增加服务器响应时间，尤其在复杂数据处理场景下。
3.  **实现难度较高：**
    
    -   需要在服务端和客户端之间共享数据逻辑，增加代码复杂性。

----------

### **总结**

服务器端渲染（SSR）是一个动态渲染解决方案，适合需要实时更新数据和高 SEO 要求的场景。虽然其性能不如 SSG，但凭借实时性和灵活性，成为动态页面和个性化内容的重要选择。结合增量静态生成（ISR），可以在性能和实时性之间找到更好的平衡。

[返回目录](#%E7%9B%AE%E5%BD%95)

### **什么是 API 路由？**

API 路由是 Next.js 提供的一种功能，用于在同一个项目中创建后端 API。通过文件系统路由机制，每个 API 文件对应一个端点 (endpoint)，允许开发者直接定义后端逻辑，供前端或其他客户端调用。

API 路由的本质是服务端的代码，运行在 Node.js 环境下，它可以处理请求、访问数据库、调用第三方 API，或进行其他后端操作。

----------

### **怎么用 API 路由？**

#### **1. 创建 API 路由**

在 Next.js 项目中，所有放置在 `pages/api` 目录下的文件都被自动映射为 API 路由。

##### 示例：创建简单的 API

```javascript
// pages/api/hello.js
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello, Next.js API!' });
}
```

-   访问路径：`http://localhost:3000/api/hello`
-   返回结果：

```json
{
  "message": "Hello, Next.js API!"
}
```

#### **2. 请求方法处理**

通过 `req.method` 判断请求类型（如 GET、POST、PUT、DELETE 等）。

##### 示例：处理不同的请求方法

```javascript
// pages/api/user.js
export default function handler(req, res) {
  if (req.method === 'GET') {
    res.status(200).json({ message: 'Fetching user data' });
  } else if (req.method === 'POST') {
    const data = req.body; // 假设前端发送 JSON 数据
    res.status(201).json({ message: 'User created', data });
  } else {
    res.setHeader('Allow', ['GET', 'POST']);
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}
```

#### **3. 动态路由**

可以通过文件名中的方括号定义动态路由。

##### 示例：动态用户 API

```javascript
// pages/api/user/[id].js
export default function handler(req, res) {
  const { id } = req.query; // 获取动态参数
  res.status(200).json({ message: `Fetching data for user ${id}` });
}
```

-   访问路径：`http://localhost:3000/api/user/123`
-   返回结果：

```json
{
  "message": "Fetching data for user 123"
}
```

#### **4. 中间件与第三方服务**

可以集成数据库、身份验证、日志等逻辑。

```javascript
import db from '../../lib/db'; // 假设有数据库连接模块

// pages/api/posts.js
export default async function handler(req, res) {
  if (req.method === 'GET') {
    const posts = await db.getPosts();
    res.status(200).json(posts);
  } else {
    res.status(405).end(`Method ${req.method} Not Allowed`);
  }
}
```

----------

### **解决了什么问题？**

1.  **全栈开发：**
    
    -   前后端在一个项目中整合，减少了开发复杂度和沟通成本。
2.  **快速原型开发：**
    
    -   无需设置单独的后端服务器，直接在项目中定义 API。
3.  **统一部署：**
    
    -   API 路由和前端页面可以一起部署到 Vercel 或其他支持 Serverless 的平台。
4.  **便捷的动态逻辑：**
    
    -   支持动态路由、身份验证、数据处理等操作，无需引入额外框架。
5.  **与 Next.js 的无缝集成：**
    
    -   API 路由可轻松与 SSR 和前端页面共享逻辑，如数据库访问层。

----------

### **有没有替代方案？**

1.  **独立后端服务：**
    
    -   使用 Express.js、Nest.js、Koa 等框架构建单独的后端服务。
    -   优点：适合复杂的后端需求，具备更高的灵活性。
    -   缺点：需要独立的部署和维护。
2.  **云函数 (Serverless Functions)：**
    
    -   使用 AWS Lambda、Vercel Functions 或 Netlify Functions。
    -   优点：按需触发、自动扩展，无需维护服务器。
    -   缺点：冷启动可能增加延迟。
3.  **GraphQL：**
    
    -   通过 Apollo Server 或其他工具构建灵活的 GraphQL API。
    -   优点：客户端可以按需查询数据，避免冗余。
    -   缺点：初学者上手较复杂。

----------

### **好处是什么？**

1.  **开发效率高：**
    
    -   同一项目即可定义后端 API，无需额外配置。
2.  **简单易用：**
    
    -   基于文件系统的路由，开发者专注于功能逻辑。
3.  **节省资源：**
    
    -   不需要额外的服务器或后端部署，只需运行 Next.js 项目即可。
4.  **自动优化：**
    
    -   支持自动热更新和 TypeScript 等特性。
5.  **灵活扩展：**
    
    -   轻松与数据库、第三方服务、身份验证系统集成。

----------

### **使用场景是什么？**

1.  **小型到中型应用：**
    
    -   API 逻辑较简单，不需要专门的后端。
2.  **原型开发：**
    
    -   快速验证产品概念或功能。
3.  **全栈应用：**
    
    -   前后端完全整合在一个项目中，例如博客、个人网站。
4.  **动态数据处理：**
    
    -   需要动态生成内容的场景，例如表单提交、用户认证。
5.  **与前端配合的后端逻辑：**
    
    -   处理用户数据、API 聚合或直接与数据库交互。

----------

### **原理是什么？**

1.  **文件系统路由：**
    
    -   `pages/api` 目录中的每个文件会映射为一个 HTTP API 路由，动态文件名映射为动态路径。
2.  **Node.js 环境：**
    
    -   API 路由运行在服务器端，使用 Node.js 提供的功能。
3.  **无状态架构：**
    
    -   每个 API 调用是无状态的，适合 Serverless 部署架构。
4.  **请求与响应：**
    
    -   API 路由接收 HTTP 请求，解析 `req` 和 `res`，并返回 JSON 数据或其他内容。
5.  **与 Next.js 集成：**
    
    -   与页面路由共享运行时环境，可直接访问共享代码（如数据库连接模块）。

----------

### **总结**

API 路由是 Next.js 的一个强大功能，适合构建轻量级后端服务或快速开发原型。通过简单的文件系统路由机制，它解决了前后端分离开发中的协调问题，同时带来了高效的开发体验。在小型应用、动态数据处理或全栈项目中，API 路由是一种便捷的选择。对于复杂的后端需求，可以考虑使用独立后端框架或云函数替代。

[返回目录](#%E7%9B%AE%E5%BD%95)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMjEzNzc4MTUsLTQyNDM0OTY4LC02Nz
Q5NzA3NDgsLTIzNDc0ODI0LDEwMDYwNjk2NTcsLTc4ODMyMDU5
Nyw0OTI5ODA4OTEsLTc4ODMyMDU5N119
-->