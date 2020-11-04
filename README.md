# @validatecl/database-manager

[![Build Status](https://travis-ci.org/validatecl/database-manager.svg?branch=main)](https://travis-ci.org/validatecl/database-manager)
![GitHub](https://img.shields.io/github/license/validatecl/database-manager)
![GitHub last commit](https://img.shields.io/github/last-commit/validatecl/database-manager)
![npm (scoped)](https://img.shields.io/npm/v/@validatecl/database-manager)
![npm](https://img.shields.io/npm/dw/@validatecl/database-manager)

Database connections manager with Mongoose.

## Installation

```sh
npm i @validatecl/database-manager
```

## Usage

It's recommended to use it as a singleton instance in your project, so you can use the manager from any module.

`./configs/database.ts`:

```ts
import { DatabaseClientConfig } from '@validatecl/database-manager';

const config: DatabaseClientConfig = {
  uri: 'mongodb://localhost:27017/test',
  options: {
    // Mongoose connection options here...
  }
};

export default [
  {
    name: 'default',
    config
  }

  // You could add more clients if necessary...
];
```

`./components/database.ts`:

```ts
import { createDatabaseManager } from '@validatecl/database-manager';

import config from '../configs/database';

const manager = createDatabaseManager();

for (let client of config) {
  manager.add(client);
}

export default manager;
```

`./some/other/module.ts`:

```ts
import db from '../../components/database';

// Ensure the 'default' client is connected...
db.connect('default');

// ...

const User = db.connection('default').model('User');
const user = await User.create({
  //...
});

// ...
```

## Documentation

Please visit [the documentation page](https://validatecl.github.io/database-manager/) for more info and options.
