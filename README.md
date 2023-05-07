# Development Documentation

## Creating a New Project

- Create a new github repo at [https://github.com/new](https://github.com/new).
  - Project name and simple description.
  - Clone the newly generated repo.
    - Navigate to the root folder for your projects.
    - Execute: `git clone git@github.com:mrzli/<project-name>.git`.
- [TODO: This will be changed after generator is more mature, and CLI is properly implemented.]
  - Use [js-project-generator](https://github.com/mrzli/js-project-generator) to create a new project.
    - Change project parameters inside `src/index.ts`. You will always want to change `projectName` and make sure you are using the proper `config`, and change it if necessary.
    - Execute `npm run start:dev` to generate project files. Unless you change the `output` parameter, the project files will be generated in the `output` folder.
    - Copy generated files from `output` folder to the root of your project.
- Prepare your project for development.
  - Open your project in IDE. If using VSCode, you can use `code <relative-path-to-project-dir>` command.
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