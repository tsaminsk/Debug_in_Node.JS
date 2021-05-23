## Найденые ошибки компиляции:

1)  ReferenceError: Router is not defined
    файл controllers\usercontroller.js, строка 1
        было: var router = Router();
        стало: var router = require('express').Router();

2)  Error: Cannot find module 'bcrypt'
    файл controllers\usercontroller.js, строка 2
        было: var bcrypt = require('bcrypt');
        стало: var bcrypt = require('bcryptjs');

3)  TypeError: require(...).import is not a function
    файл controllers\usercontroller.js, строка 5
        было var User = require('../db').import('../models/user');
        стало const User = require('../models/user');

4)  TypeError: require(...).import is not a function
    файл controllers\gamecontroller.js, строка 2
        было var Game = require('../db').import('../models/game');
        стало const Game = require('../models/game');

5)  ReferenceError: routers is not defined
    файл controllers\gamecontroller.js, строка 116
        было module.exports = routers;
        стало module.exports = router;

6)  TypeError: require(...).import is not a function
    файл \middleware\validate-session.js, строка 2
        было    var User = require('sequelize').import('../models/user');
        стало   const { sequelize, DataTypes } = require('../db');
                const User = require('../models/user')(sequelize, DataTypes);

7) обновление модулей (зависимостей) в проекте до актуальных версий

==================================

## Найденные ошибки логики приложения

1)  файл models/game.js ошибка экспорта
        было: function(sequelize, DataTypes) {
        стало: module.exports = function (sequelize, DataTypes)

2)  ошибка экспорта
    файл db.js стр. 20 добавлен module.exports = { sequelize, DataTypes: Sequelize.DataTypes };

3)  TypeError: db.sync is not a function
    файл **app.js** исправлено строка 9
        ```db.sequelize.sync();```

4)  notNull Violation: user.passwordHash cannot be null
    файл **controllers\usercontroller.js** стр.12 passwordhash => passwordHash

5)  файл **controllers\gamecontroller.js** строка 9
        было function findSuccess(data)
        стало function findSuccess(games)

6)  файл **controllers\gamecontroller.js** строка 76
        было owner_id: req.user
        стало owner_id: req.user.id

=======================================

## Рефактор кода

3.  обозначение переменных **var** заменено на более современные **let** & **const**

3.  добавлены **;** и **,** в конце строк где это необходимо

3.  добавленна деструктуризация где это возможно, например:
<table>
    <tr>
        <td>Было</td>
        <td>Стало</td>
    </tr>
    <tr>
        <td>
            ```function deleteFail(err) {
                res.status(500).json({
                    error: err.message
                })
            }```
        </td>
        <td>
            ```function deleteFail({ message }) {
                res.status(500).json({ error: message });
            }```
        </td>
    </tr>
</table>
