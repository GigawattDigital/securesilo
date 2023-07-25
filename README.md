# securesilo

Private AI Server

## What is securesilo?

securesilo is a private AI server that you can run on your own hardware or in the cloud.

Organizations that want to use AI to generate content, but are concerned about the privacy and security
of their data, can use securesilo to create a private AI server that is completely under their control.

Using 100% open source software, securesilo provides a secure, end-to-end encrypted service that your
users can access via a web-based bot, a command line client, mobile app, or via the securesilo API
_**without having to worry about any of your prompt data or ai-generated content being shared with any
third party**_.

## How secure is securesilo?

securesilo uses end-to-end encryption to ensure that your data is secure at all times. All prompt data
is encrypted on the client device before it is sent to the server, all responses are encrypted on the
server before being sent back to the user's device, and all data stored on the server is encrypted at
rest.

When you create a securesilo server instance, you generate a public/private key pair that is used to
encrypt your data for storage on the file system or in the database.  The private key is never stored
on the server, so only you can access your data.  The silo can write this encrypted data but cannot
decrypt it once it is written.  Users' private keys can decrypt their own data on their devices, and
the administrator's private key can decrypt all data on the server but, again, the decryption happens
on the administrator's client device, not on the server.

You can also create backup private keys that can be used to recover your data in the event that you
lose access to your primary private key. Backup private keys are unique keys that can be stored in
secure offsite locations or with trusted third parties.  You can create as many backup private keys
as you like to ensure that you can always recover your data.  Any backup private key can be revoked
at any time.

You control who can access all chat logs and ai-generated content stored on the server, and you can
revoke user access at any time.  Since all data is encrypted both in transit and at rest, even if
your server is compromised, all stored data remains encrypted and can only be recovered only by
using the administrator's private key or a backup private key.

## What if I lose my private key?

_If you lose your private key and do not have backup private keys, your data will be lost forever!
Due to the nature of public key encryption, there is no way to recover your data without the one of
the private keys that were used to encrypt it._

**Therefore, if your data has significant financial value or business operational risk, it is
strongly recommended that you create at least three backup private keys and store them in
different secure offsite locations (such as a on a thumb drive in a safety deposit box at a bank)
and/or with trusted third parties such as your attorney, accountant, audit firm, professional key
escrow service, professional security firm or other trusted individuals.  Private keys can also be
printed out on paper or stored securely on a hardware security device such as a Yubikey or Trezor.**

Each user that you create on your server instance is assigned a unique device-based passkey that is
used to encrypt their data in transit.  User passkeys are generated on the user's device and are
never sent to the server.  The server only stores the public key portion of the user's passkey.
In addition, user passkeys are rotated on a regular basis to ensure that even if a user's device is
compromised, the risk of data loss is limited.  You can also require users to use two-factor
authentication to further secure their account.

## Is it as good as OpenAI?

securesilo uses only LLM's (large language models) that have been released as open source software,
or with a license that allows for commercial use, that can be run entirely on your own hardware or
a cloud server that you completely control, without having to rely on any third party service which
could use your data for their own purposes.

Currently securesilo supports:

### Meta's llama-2 engine

llama-2 is a powerful engine that can be used to generate a wide variety of content.  While it is not
quite as powerful as OpenAI's GPT-4, it already outperforms the GPT-3.5, Bing and Bard engines on most
tasks.  Notably, llama-2 does not (yet!) generate images or computer language code, but it generates
text responses to natural language queries very well, and is quite suitable for generating text-based
documents such as technical reports, articles, scientific research, contracts and other legal documents.

Additional language models are the roadmap such as

- other Open LLMs <https://github.com/eugeneyan/open-llms>

And we plan to add support for _non-text_ LLMs soon such as

- text-to-image models such as DALL-E, CLIP, VQGAN, and others
- code generation models such as Codex and Copilot

## How much does it cost?

securesilo is 100% free, open source software.  It is licensed under the MIT license, so you can
use it for any purpose you like.

The Llama 2 language model can be licensed for commercial use from Meta as long as you agree to their
License Agreement <https://ai.meta.com/resources/models-and-libraries/Llama-downloads/> and
Acceptable Use Policy <https://ai.meta.com/llama/use-policy/>

## Can I use it for commercial purposes?

Anyone can use securesilo for any purpose they like, including commercial use.  Distribution of the
securesilo software is subject to the open source terms of the MIT license.

The Llama 2 language model can be licensed for commercial use from Meta, at no cost _as long as you have
fewer than 700 million active users per month_ 😮 and do not use it to train other LLM's.

For research use, there is no limit on the number of users.

## Can I train it with my own data?

securesilo is designed to use pre-trained language models, See PLUGINS (and RELATED PROJECTS) below for
links to the software, tools and and hardware needed to train your own language models.

## Plugins

securesilo supports plugins that can be used to extend its functionality.  Plugins can be used to
add new language models, user interfaces, structured document types and data formats, storage
methods locations, encryption methods, and visualization tools that we could never dream up on
our own.

You can create your own plugins, use plugins contributed by the community or purchase proprietary
plugins from third parties.  You can also sell your own plugins to other securesilo users on the
soon-to-be-released securesilo plugin marketplace.

## How do I get started?

There are two ways to get a securesilo server instance up and running:

### DFY (Done For You)

For a turn-key solution, you can use [securesilo's Done For You service](https://securesilo.ai/plans)
to have a securesilo server instance created and professionally hosted for you on our infrastructure.

### DIY (Do It Yourself)

If you want to run your own server, you can use the instructions below to get started.

## Hardware Requirements

- server with at least 16GB of RAM
- an NVIDIA GPU with at least 8GB of RAM

Examples of minimum cloud instances types/sizes that meet these requirements are:

- Amazon AWS EC2 g4dn.2xlarge instance (8 vCPU, 32GB RAM, 1x 125GB NVMe SSD, 1x NVIDIA T4 GPU)
- Google Cloud GCE n1-standard-8 instance (8 vCPU, 30GB RAM, 1x 100GB SSD, 1x NVIDIA T4 GPU)
- Microsoft Azure NCasT4_v3 instance (8 vCPU, 32GB RAM, 1x 100GB SSD, 1x NVIDIA T4 GPU)

## OS Platform

securesilo has been tested on the following platforms:

- Rocky Linux 8.4
- CentOS 8.4
- Ubuntu 20.04 LTS
- Ubuntu 21.04
- MacOS 11.5.2

## Software requirements

securesilo requires the following software to be installed on your server:

- Docker
- Docker Compose
- Git
- Python 3.8 or later
- pyTorch 1.9 or later
- CUDA 11.1 or later
- cuDNN 8.2 or later
- NVIDIA GPU driver 470.57.02 or later

## Install Docker

See the [Docker installation guide](https://docs.docker.com/engine/install/) for instructions on how to
install Docker on your server.

## Install Docker Compose

See the [Docker Compose installation guide](https://docs.docker.com/compose/install/) for instructions
on how to install Docker Compose on your server.

## Install Git

See the [Git installation guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) for

## Install Python 3.8 or later

See the [Python installation guide](https://www.python.org/downloads/) for instructions on how to

## Install pyTorch 1.9 or later

See the [pyTorch installation guide](https://pytorch.org/get-started/locally/) for instructions on how to

## Install CUDA 11.1 or later

See the [CUDA installation guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)

## Install cuDNN 8.2 or later

See the [cuDNN installation guide](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html)

## Install NVIDIA GPU driver 470.57.02 or later

See the [NVIDIA GPU driver installation guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html)

## Clone the securesilo repository

```bash
git clone git@github.com:GigawattDigital/securesilo.git
```

## Configure your Meta commercial license

Copy the `env.example` file in the project root directory to ``.env`` and edit the values to provide
your Meta llama-2 license information.

(please use your own values for the license keys, not the invalid sample values shown below)

```bash

# meta llama2 license info
SILO_META_Key_Pair_Id=K15QTJFJEIFSLZ
SILO_META_Policy=eyJTdGF0ZW1lbnRiOlt7InVuaXF1ZV9eYXNoIjoiXHUwMDAxP1Q%7EVT8jWyIsIlJlc791cmNlIjoiaHR0cHM6XC9oL2Rvd25sb2FkLmxsNW1hbWV0YS5uZXRcLyoiLCJDb25khXRpb24iOnsiRGF0ZUxlc3NUaGFuIjp7IkFXUzpFcG9jaFRpbWUiOjE2ODk4OTg4NjF9fX1dfQ__
SILO_META_Signature=jKj8w2K5uNW4fuDyj9QMSvLsOMZMydJk5-sAlHwIK40EctKgFpP-bHvGIgEwPnfdc%7EMxh85b8olqPtK4bYk0Jiuv1Q3ZIeg-j0wrtQAvozi8w5OyB9G-lwjiwQx2A-kCjbgdkWP0DZSXM-gCapk4sskfzMkjRwiveqT2Yw7hP16Oy04RHbK6Jgglaxc4hdiSM0X9aMhZN1ExyD%7EX8arqanP8HkBVb9exSiavtWhsn%7EyzratAEA2soVZApb07H74GU2S%7EPh3xIHk8I%7EtsZsgeVihGa1w6jZB7ayugmigz9z%7E%7EPAdK3x6WXSeLj4cjgwciiFXKZIqH-uOkCXHDY-e71g__

# Optionally, change the hostname/ip and/or and port you'd like to use to access your development instance
SILO_HOST=localhost
SILO_PORT=6006

```

## Run the docker container

```bash
docker-compose up
```

## Login to you personal AI server

Open a browser and navigate to [http://localhost:6006/](http://localhost:6006/) (or whatever
host/port you configured in your `.env` file)

Create your admin account and setup its userid and password.

## Generate the public and private keys that will be used to encrypt your data at rest on the server

Be sure to save the private key file in a safe place.  You will need it to decrypt your data.
Only the public key will be stored on the server.

## Start generating secure content

That's it!  You're ready to start creating AI-generated content.

All of your prompt and ai-generated data will be end-to-end encrypted so that, even if the server is
compromised, your data will be safe.

### Clients

#### the web-based bot

securesilo includes a web-based interactive prompt interface gigabot that you can use to generate
content.

gigabot is a clone of the popular OpenAPI bot, but runs locally in your browser and connects to your
securesilo server instance instead of OpenAI's servers.

All communication between your browser and your securesilo server instance is encrypted,
your prompts are encrypted before they are sent to the server, stored encrypted on the server,
and all ai-generated responses are encrypted before beng sent back to your browser.

#### the command line client

securesilo also includes a command line client that you can use to create and manage ai-generated files.

#### API access

You can also access your securesilo server instance via the securesilo API.  The securesilo api is
compatible with the OpenAI API, so you can use the same tools you use with OpenAI to access your
securesilo server instance.

## Production deployment

Since securesilo is designed to use end-to-end encryption, deploying to a publicly accessible server is
nearly identical to setting up development instance.

The only differences are that you will need to configure the `.env` file with the URL of your server,
and enforce the use of SSL.

See the [securesilo user guide](https://securesilo.ai/docs/user-guide) for more information on how to
require users to use two-factor authentication, device-based passkeys, and control other user-related
security settings.  New users can also be required to register using an email with a specified domain
and/or only allow users to be created via an invitation link.

```bash

# allow only SSH access to securesilo instance
SILO_SSL_MODE=1

# set the public URL of your server
SILO_URL=https://mysilo.mydomain.com

```

If your silo is running behind a reverse proxy that provides SSL termination (like a local nginx server,
AWS ELB load balancer or remote reverse proxy service such as Cloudflare), you can set SILO_URL to an https
URL e.g. `https://mysilo.mydomain.com` along with a `SILO_SSL=0` setting. Silo will detect the `https://`
protocol of the URL and prompt you to confirm that you want to use https URL's even though it is running
in http mode.  While this could be considered slightly less secure, as traffic between your host and
the (possibly distant) reverse proxy will be unencrypted at the network level, the risk is insignificant
because all traffic between your users' devices and the securesilo instance is still end-to-end encrypted
at the application level, in transit, and at rest on the server.  So the risk of a person-in-the-middle
attack is limited to that person (such as staff at your hosting provider, at your users' internet providers,
Cloudflare, or any of the untrusted networks in-between) being able to see _that communication is occurring_
between your web server and the reverse proxy.  The content of that communication will still be encrypted.

See the [securesilo deployment guide](https://securesilo.ai/docs/deployment) for more advanced deployment
configuration options.

## Related Projects

- Langchain - Chaining multiple LLMs to one another
  <https://github.com/langchain-ai/langchain>

- Chroma - embed a corpus of PDF documents for search and retrieval
  <https://github.com/chroma-core/gpt4-pdf-chatbot-langchain-chroma>

- Llama Index - Connect LLMs to external data sources
  <https://github.com/jerryjliu/llama_index>

- ChatGPT Retrieval Plugin
  <https://github.com/chroma-core/chatgpt-retrieval-plugin>

- Copilot for lawyers
  <https://www.harvey.ai/>

- GPT4All - federated inference using consumer grade CPUs
  <https://github.com/nomic-ai/gpt4all>

- Falcon MPT - Powerful Open-Source Language Model
  <https://www.mosaicml.com/blog/mpt-30b>

- Vicuna - Open Source Chat Bot tuned for conversation
  <https://github.com/eddieali/Vicuna-AI-LLM>

- Stable Diffusion Image models
  <https://github.com/Stability-AI/stablediffusion>

- Awesome Transformers - A curated list of awesome transformers and pre-trained models
  <https://github.com/huggingface/transformers/blob/main/awesome-transformers.md>

