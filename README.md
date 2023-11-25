# Agenda

## Introduction

- Short introduction of azd (what is it, how can it help you)
- How to use it in your projects

## Greenfield project

Starting from scratch using the templates

- Show templates
- Create an instance of templates with short walk through
- shortly walk through template ... maybe deploy one

But you to use our own templates?

- How to customize the templates
- azd template source add
- How should the file look like?

```bash
azd template source list
```

https://azure.github.io/awesome-azd/templates.json => this is not the format :-)

The right format is: https://github.com/Azure/azure-dev/blob/main/cli/azd/resources/templates.json

```bash
azd template source remove awesome-azd
```

```bash
azd template source add dapr-aca --type url --location https://raw.githubusercontent.com/lechnerc77/azd-festive-tech-calendar-2023/main/custom_template/dapr_template.json
```

Attention with --file: The file path must be available from wherever you call the azd

Open question .. how to handle authentication if it is a private repo, blob storage etc.

Always come back to standard via:

```bash
azd template source add awesome-azd
```

## Brownfield

We have existing projects (we all have, right?) - so how to get started?

## Option 1

- azd - the hard way: Do it yourself based on a template aka "copy&paste&adjust" (using minimal starter templates)
- However this way you learn a lot about how azd works

## Option 2

- azd easy init ... entering the stage
- Restrictions: ACA only

How does it work => debug in dev container:

`cli\azd\cmd\init.go` line 222 => Init from app
`cli/azd/internal/repository/app_init.go` => line 45
`cli\azd\internal\appdetect\appdetect.go` => line 170

Logic of app detectors is in cli\azd\internal\appdetect => one per language; .NET devs be aware of the comments

`cli\azd\internal\appdetect\javascript.go` => line 26

Let's see this in action

- But wait a moment ... if it is ACA and we do not have a Dockerfile, how does it build a container?
- Cloud Native Build Packs for the rescue

`cli\azd\cmd\package.go` => line 108 + 198

`cli\azd\pkg\project\framework_service_docker.go` => 143 , 173, 183, 274, 353

`cli\azd\pkg\tools\pack\pack.go` => 283