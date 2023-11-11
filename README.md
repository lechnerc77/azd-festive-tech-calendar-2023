# Agenda

## Introduction

Short introduction of azd (what is it, how can it help you)

How to use it in your projects

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

We have existing projects (we all have, right) - so how to get started?

## Option 1

- azd - the hard way: Do it yourself based on a template aka "copy&paste&adjust"
- However this way you learn a lot about how azd works

## Option 2

- azd easy init ... entering the stage
- Restrictions: ACA only

How does it work:

cli/azd/internal/repository/app_init.go

=> debug in dev container

Cloud Native Build packs

cli/azd/pkg/project/framework_service_docker.go