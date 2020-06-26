# Welcome to the Frontend Contributing Guide!

Before contributing, please read the [code of conduct](https://github.com/HospitalRun/hospitalrun/blob/master/.github/CODE_OF_CONDUCT.md).

## 1. Check out the [HospitalRun General Contributing Guide](https://github.com/HospitalRun/hospitalrun/blob/master/.github/CONTRIBUTING.md) for how to:
   1. Browse Issues
   2. Get Assigned an Issue
   3. Fork the Repository and Create a Branch
   4. Commit Changes
   5. Submit a Pull Request

## 2. After creating a local branch (step 3 above), follow these steps to configure CouchDB

CouchDB is the server side database which data from the frontend will sync to. CouchDB is required to login
to HospitalRun. You could install and run CouchDB in any way you wish. For convienence, we have added a docker compose file in the
root of this project to launch CouchDB. Below is the steps:

1. Start [Docker](https://docs.docker.com/get-docker/). Install it if you don't have it yet.
2. Install [Docker Compose](https://docs.docker.com/compose/install/) if you don't have it yet.
3. Run `docker-compose up --build -d` in the root directory.

Note: This should launch a new CouchDB instance on `http://localhost:5984`, create system database, configure CouchDB as Single Node, enable CORS, create `hospitalrun` database, create a default admin with a username of `admin` and password of `password`

4. Run this command if you have not created a user yet:
   ```
   curl -X PUT http://admin:password@localhost:5984/_users/org.couchdb.user:username -H "Accept: application/json" -H "Content-Type: application/json" -d '{"name": "username", "password": "password", "metadata": { "givenName": "John", "familyName": "Doe"}, "roles": [], "type": "user"}'
   ```
Note: This should create a user with username/password of `username`/`password`.

Note: Go to `http://localhost:5984/_utils` in your browser to view Fauxton and perform administrative tasks.

5. Open a file named `.env` and add a line `REACT_APP_HOSPITALRUN_API=http://localhost:5984` if you don't have it yet.

_Note: To delete the development database, go to the root of the project and run `docker-compose down -v --rmi all --remove-orphans`_

## 3. Test locally
Every push to a remote branch triggers a test. The same test can be performed locally as below.

`npm run test:ci` will run the entire test suite

`npm run test:ci <file name>` e.g. `npm run test:ci src/__tests__/HospitalRun.test.tsx` will run that specific test file

`npm run test` will run the test suite in watch mode

## 4: Run linter locally
`npm run lint` will run the linter

`npm run lint:fix` will run the linter and fix fixable errors

## Useful Developer Tools

- [VSCode](https://code.visualstudio.com/)
- [VSCode React Extension Pack](https://marketplace.visualstudio.com/items?itemName=jawandarajbir.react-vscode-extension-pack)
- [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
- [Redux Developer Tools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en)

## Resources
- For a list of language codes we use, see [this](https://github.com/HospitalRun/hospitalrun-frontend/tree/master/src/locales/README.md).
