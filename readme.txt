name: Multi-Repository Build

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      # Trigger builds in other repositories using repository_dispatch
      - name: Trigger Build in pollux
        uses: peter-evans/repository-dispatch@v1
        with:
          repository: constellation/pollux
          event-type: build

      - name: Trigger Build in capella
        uses: peter-evans/repository-dispatch@v1
        with:
          repository: constellation/capella
          event-type: build

