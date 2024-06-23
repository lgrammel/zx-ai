# zx-ai

Quick guide how to use the [Vercel AI SDK](https://sdk.vercel.ai) with [ZX](https://github.com/google/zx) to create executable Node.js scripts that use AI.

1. [Install zx (e.g. with brew)](https://google.github.io/zx/getting-started#install)
1. Install
    ```sh
    npm i ai @ai-sdk/openai dotenv
    ```
1. Add OpenAI API key to `.env` (`OPENAI_API_KEY`)
1. Write a `.mjs` script (e.g. `hello-world.mjs`)
   ```ts
   #!/usr/bin/env zx

   import { openai } from "@ai-sdk/openai";
   import { streamText } from "ai";
   import { configDotenv } from "dotenv";

   configDotenv();

   const { textStream } = await streamText({
     model: openai("gpt-4o"),
     prompt: "How can I list files in bash?",
   });

   for await (const textPart of textStream) {
     process.stdout.write(textPart);
   }
   ```
1. Make executable: `chmod +x hello-world.mjs`
1. Run: `./hello-world.mjs`