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
      - name: Trigger Build in Repository A
        uses: peter-evans/repository-dispatch@v1
        with:
          repository: repository-a-owner/repository-a
          event-type: build

      - name: Trigger Build in Repository B
        uses: peter-evans/repository-dispatch@v1
        with:
          repository: repository-b-owner/repository-b
          event-type: build

