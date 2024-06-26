# AnyNode v0.1 (🍄 beta)

A ComfyUI Node that uses the power of LLMs to do anything with your input to make any type of output.

![image](https://github.com/lks-ai/anynode/assets/163685473/43043c8f-24f6-4693-bc9e-43666cda78b3)

![image](https://github.com/lks-ai/anynode/assets/163685473/a0596d98-911e-4a93-b0f7-6f6a8782d49d)

[![Watch the video](https://img.youtube.com/vi/f52K5pkbZy8/maxresdefault.jpg)](https://youtu.be/f52K5pkbZy8)

### [📺 More Tutorials on AnyNode at YouTube](https://www.youtube.com/watch?v=f52K5pkbZy8&list=PL-EiB44NKrkcxJnR9MwD4hOSZOTlHn6Tr)

## Update: Day 3 - Local LLMs Generating Nodes!
![Screenshot from 2024-05-27 13-32-58](https://github.com/lks-ai/anynode/assets/163685473/70cb508e-b2af-470a-b777-1ddebe1cd59c)
We now have an `AnyNode 🍄 (Gemini)` Node and our big star: The `AnyNode 🍄 (Local LLM)` Node.
This was the most requested feature since Day 1. The classic `AnyNode 🍄` will still use OpenAI directly.
- You can set each LocalLLM node to use a different local or hosted service as long as it's OpenAI compatible
- This means you can use [Ollama](https://ollama.com/), [vLLM](https://github.com/vllm-project/) and any other LocalLLM server from wherever you want

## Install: Update (We just got on ComfyUI Manager!)

1. Clone this repository into `comfy/custom_nodes` *or* Just search for `AnyNode` on ComfyUI Manager
2. If you're using openAI API, follow the OpenAI instructions
3. If you're using Gemini, follow the Gemini Instructions
4. If you're using LocalLLMs API, make sure your LLM server (ollama, etc.) is running
5. Restart Comfy
6. In ComfyUI double-click and search for `AnyNode` or you can find it in Nodes > utils

### OpenAI Instructions
1. Make sure you have the `openai` module installed through pip: `pip install openai`
2. Add your `OPENAI_API_KEY` variable to your Environment Variables. [How to get your OpenAI API key](https://platform.openai.com/docs/quickstart)

`AnyNode 🍄` Is the node that directly uses OpenAI with the latest ChatGPT (whichever that may be at the time)

### Gemini Instructions
1. You don't need any extra module, so don't worry about that
2. Add your `GOOGLE_API_KEY` variable to your Environment Variables. [How to get your Google API key](https://aistudio.google.com/app/apikey)

`AnyNode 🍄 (Gemini)` is still being tested so it probably contains bugs. I will update this today.

### A Note about Security for the Local LLM variant
The way that AnyNode works, is that it executes code which happens externally from python that is coming back from the `server` on a ChatCompletions endpoint. To put that into perspective, wherever you point it, you are giving some sort of control in python to that place. **BE CAREFUL** that if you are not pointing it to `localhost` that you absolutely trust the address that you put into `server`.

## How it Works

1. Put in what you want the node to do with the input and output.
2. Connect it up to anything on both sides
3. Hit `Queue Prompt` in ComfyUI

AnyNode codes a python function based on your request and whatever input you connect to it to generate the output you requested which you can then connect to compatible nodes.

![image](https://github.com/lks-ai/anynode/assets/163685473/1245aa94-fa4d-4490-a3f4-5e8b9918ca28)

**Warning**: Because of the ability to link *ANY* node, you have to make sure it nails the output. 

## Caveats
- I have no idea how far you can take this nor it's limits
- LLMs can't read your mind. To make complex stuff in one node you'd have to know a bit about programming
- The smaller the LLM you use to code your nodes, the less coding skills it might have
- Right now you can only see code the LLM generates in the console
- Can't make a sandwich

## Strengths
- Use OpenAI `AnyNode 🍄`, Local LLMs `AnyNode 🍄 (Local LLM)`, Gemini `AnyNode 🍄 (Gemini)`
- You can use as many of these as you want in your workflow creating possibly complex node groups
- Really great at single purpose nodes
- Uses OpenAI API for simple access to the latest and greatest in generation models
- Technically you could point this at vLLM or Ollama for you LocalLLM fans
- Can use most of the popular python libraries and most standard like (numpy, torch, collections, re)
- Ability to make more complex nodes that use inputs like MODEL, VAE and CLIP with input type awareness
- Error Mitigation: Auto-correct errors it made in code (just press `Queue Prompt` again)
- Incremental Code editing (the last generated function serves as example for next generation)
- Copying cool nodes you prompt is as easy as copying the workflow

## Coming Soon
- **Export to Node**: Compile a new comfy node from your AnyNode (Requires restart to use your new node)
- Saving the generated functions in your workflows
- Multiple Inputs and outputs
- RAG based function storage and semantic search across comfy modules (not a pipe dream)
- Persistent data storage in the AnyNode (functions store extra data for iterative processing or persistent memory)

## Known Coding Errors you Might Encounter
As with any LLMs or text generating language model, when it comes to coding, it can sometimes make mistakes that it can't fix by itself even if you show it the error of it's ways. A lot of these can be mitigated by modifying your prompt. If you encounter some of the known ones, we have some prompt engineering solutions here for you.

### `invalid syntax (, line 1)`
If you've used ChatGPT, you know the output can be rather chatty. That being said, sometimes when AnyNode runs, you will see this ambiguous error. So without you having to check the console I'll just tell you... it's the chattyness. What happens is the LLM tries to talk to you.  This can be mitigated by re-inforcing your prompt with `Quit yapping. Only write the function.` at the very end.  We've reinforced it in the latest updates, but yes, there is also a deeper fix to do, which just ignores the chattyness. Only, I'd rather it never be chatty, because that tends to make it do other things which don't make sense. We're looking for strict rule following here, and not random creativity.

## If you're still here
Let's enjoy some stuff I made while up all night!

![image](https://github.com/lks-ai/anynode/assets/163685473/02801f5c-9f67-40f1-83a7-a93e6103d362)
This one, well... the prompts explain it all, but TLDR; It takes an image as input and outputs only the red channel of that image.

![Screenshot from 2024-05-26 01-30-40](https://github.com/lks-ai/anynode/assets/163685473/4cfe5b0b-d515-4f9d-9d86-eff1a08595ed)
Here I use three AnyNodes: One to load a file, one to summarize the text in that file, and the other to just do some parsing of that text. No coding needed.

![image](https://github.com/lks-ai/anynode/assets/163685473/4bc5c6c0-ca56-4f4c-88d5-5339b6d5ada1)
I took that Ant example a bit further and added in the normal nodes to do img2img with my color transforms from AnyNode

![Screenshot from 2024-05-26 20-45-57](https://github.com/lks-ai/anynode/assets/163685473/0e02ae11-7e46-4d50-8645-fe7a5d3c46c9)
Here I ask for an instagram-like sepia tone filter for my AnyNode ... I titled the node Image Filter just so I can remember what it's supposed to be doing in the workflow

![image](https://github.com/lks-ai/anynode/assets/163685473/b8879685-6a78-4314-a8e4-5d88d046621d)
Let's try a much more complex description of an HSV transform, but still in plain english. And we get a node that will randomly filter HSV every time it's run!
[Here's that workflow](workflows/anynode_hsl-tweak.json)

![Screenshot from 2024-05-26 21-05-25](https://github.com/lks-ai/anynode/assets/163685473/c00531c9-c93a-471a-bca0-bb62abea4943)
Then I ask for a more legacy instagram filter (normally it would pop the saturation and warm the light up, which it did!)

![image](https://github.com/lks-ai/anynode/assets/163685473/dda13811-7e0e-4d9e-ab7c-fd2ff3d594ba)
How about a psychedelic filter?

![image](https://github.com/lks-ai/anynode/assets/163685473/29db4cd9-db77-4931-a340-10755e0211fa)
Here I ask it to make a "sota edge detector" for the output image, and it makes me a pretty cool Sobel filter. And I pretend that I'm on the moon.
[Here's that workflow](workflows/sobel-charcoal.json)
