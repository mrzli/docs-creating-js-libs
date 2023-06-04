# Development Documentation

## Creating a New Project

- Generate the new project using `jsgen`.
  - See more information at [https://github.com/mrzli/js-project-generator-cli](https://github.com/mrzli/js-project-generator-cli).
  - Make sure you have the proper configuration.
    - Default configurations can be set at `~/.jsgen.config.json` and `./jsgen.config.json` (will be merged, with latter taking precedence).
    - Any configuration set with `-c`.
    - Any configuration options passed as other command line arguments.
      - You will want to set `projectType`, `projectName` and possibly `output` (output directory).
  - Execute `jsgen` to generate the project.
    - Example: `jsgen -t node -p my-project -o _node-util`.
- Create a new github repo at [https://github.com/new](https://github.com/new).
  - Set project name and simple description.
  - Clone the newly generated repo.
    - Navigate to the root folder for your projects.
    - Execute: `git clone git@github.com:mrzli/<project-name>.git`.
  - Add project to [repos](https://github.com/mrzli/repos) readme, and push `repos` changes to github.
- Prepare your project for development.
  - Open your project in IDE. If using VSCode, you can use `code <relative-path-to-project-dir>` command.
  - Setup git.
    - Navigate to the root directory of your project.
    - Execute `git init` to initialize git.
    - Execute:
      - `git remote add origin git@github.com:mrzli/<project-name>.git`.
    - In case you already have a different `origin` set up, execute:
      - `git remote set-url origin git@github.com:mrzli/<project-name>.git`.
  - Execute `npm install` to install all dependencies.
- Make initial updates.
  - Update `description` in `package.json`.
  - Update `README.md` file.

## Making Updates to the Project

- Make any changes you need to to the project.
- [TODO: It will probably make sense to create git tags for each version.]
- Update `README.md` file if necessary.
- Update `CHANGELOG.md` file.
- Update `version` in `package.json`.
- Commit and push your changes to github.
- Execute `npm run pub` to publish your changes to npm.