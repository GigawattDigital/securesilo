# securesilo
Private AI Server

## What is securesilo?

securesilo is a private AI server that you can run on your own hardware or in the cloud.

Organizations that want to use AI to generate content, but are concerned about the privacy and security
of their data, can use securesilo to create a private AI server that is completely under their control.

Using 100% open source software, securesilo provides a secure, end-to-end encrypted service that your
users can access via a web-based bot, a command line client, mobile app, or via the securesilo API
without having to worry about any of your prompt data or ai-generated content being shared with any
third party.

## How secure is securesilo?

securesilo uses end-to-end encryption to ensure that your data is secure at all times. All promt data
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
revoke access at any time.  Since all data is encrypted both in transit and at rest, even if your
server is compromised, all stored data remains encrypted and can only be recovered by use of the
administrator's private key or a backup private key.

Each user that you create on your server instance is assigned a unique device-based passkey that is
used to encrypt their data in transit.  User passkeys are generated on the user's device and are
never sent to the server.  The server only stores the public key portion of the user's passkey.
In addiiton, user passkeys are rotated on a regular basis to ensure that even if a user's device is
compromised, the risk of data loss is limited.  You can also require users to use two-factor
authentication to further secure their account.

## Is it as good as OpenAI?

securesilo uses only LLM's (large anguage models) that have been released as open source software,
or with a license that allows for commercial use, that can be run ebntirely on your own hardware or
a cloud server that you completely control, without having to rely on any third party service which
could use your data for their own purposes.

Currently securesilo supports:

**Meta's llama-2 engine**

llama-2 is a powerful engine that can be used to generate a wide variety of content.  Earlyy reports
suggest that, whie it is not quite as powerful as OpenAI's GPT-4, it already outperforms GPT-3.5,
Bing and Bard engines on most tasks.  Notably, llama-2 does not (yet!) generate computer language code
or images, but it generates text responses to natural language queries very well.

Additional language models are the roadmap such as

- other Open LLMs https://github.com/eugeneyan/open-llms

And we hope to add support for _non-text_ LLMs soon such as

- text-to-image models such as DALL-E, CLIP, VQGAN, and others
- code generation models such as Codex and Copilot

## How do I get started?

There are two ways to get a securesilo server instance up and running:

### DFY (Done For You)

If you don't want to worry about setting up and maintaining your own server, you can use
[securesilo's Done For You service](https://securesilo.ai/plans) to have a securesilo server instance
created and managed for you **on your own Amazon AWS account**.

We can also create and manage your server instance on your hardware or on any cloud provider
that offers the necessary NVIDEA GPU processing power and RAM needed for AI, such as (currently)
[Google Cloud GCE](https://cloud.google.com/gpu/),
[Microsoft Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes-gpu) or
[Linode GPU](https://www.linode.com/products/gpu/)

Digital Ocean and other cloud providers' GPU compute offerings will be supported as they become available.

Your DYF server instance will be created **on your own account**, so you will have full control over it,
as well as all of your data.  We do not resell cloud services, so you will be billed directly by your
cloud provider for the services you use.

### DIY (Do It Yourself)

If you want to run your own server, you can use the instructions below to get started.

## Hardware Requirements

- server with at least 16GB of RAM
- an NVIDEA GPU with at least 8GB of RAM

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

Copy the `env.example` file in the project root directory to `.env` and edit the values to provide 
your Meta llama-2 license information.

(please use your own values for the licence keys, not the invalid sample values shown below)

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
host/port you configured in your .env file)

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

securesilo includes a web-based bot that you can use to generate content named gigabot.

gigabot is a clone of the popular OpenAPI bot, but it runs locally in your browser.

All communication between your broeser and your securesilo server instance is encrypted,
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

The only differencees are that you will need to configure the .env file with the URL of your server,
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
URL e.g. https://mysilo.mydomain.com along with a SILO_SSL=0 setting. Silo will detect the https://
protocol of the URL and prompt you to confirm that you want to use https URL's even though it is running
in http mode.  While this could be considered slighty less secure, as traffic between your host and
the (possibly distant) reverse proxy will be unencrypted at the network level, the risk is insignificant
because all traffic between your users' devices and the securesilo instance is still end-to-end encrypted
at the application level, in transit, and at rest on the server.  So the risk of a person-in-the-middle
attack is limited to that person (such as staff at your hosting provider, at your users' internet providers,
Cloudflare, or any of the untrusted networks in-between) being able to see _that communication is occuring_
between your web server and the reverse proxy.  The content of that communication will still be encrypted.

```bash

```bash

See the [securesilo deployment guide](https://securesilo.ai/docs/deployment) for more advanced deployment
configuration options.

