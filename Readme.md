## Найденые ошибки компиляции:

1)  ReferenceError: Router is not defined<br />
    файл controllers\usercontroller.js, строка 1<br />
        было: var router = Router();<br />
        стало: var router = require('express').Router();

2)  Error: Cannot find module 'bcrypt'<br />
    файл controllers\usercontroller.js, строка 2<br />
        было: var bcrypt = require('bcrypt');<br />
        стало: var bcrypt = require('bcryptjs');

3)  TypeError: require(...).import is not a function<br />
    файл controllers\usercontroller.js, строка 5<br />
        было var User = require('../db').import('../models/user');<br />
        стало const User = require('../models/user');

4)  TypeError: require(...).import is not a function<br />
    файл controllers\gamecontroller.js, строка 2<br />
        было var Game = require('../db').import('../models/game');<br />
        стало const Game = require('../models/game');

5)  ReferenceError: routers is not defined<br />
    файл controllers\gamecontroller.js, строка 116<br />
        было module.exports = routers;<br />
        стало module.exports = router;

6)  TypeError: require(...).import is not a function<br />
    файл \middleware\validate-session.js, строка 2<br />
        было    var User = require('sequelize').import('../models/user');<br />
        стало   const { sequelize, DataTypes } = require('../db');<br />
                const User = require('../models/user')(sequelize, DataTypes);

7) обновление модулей (зависимостей) в проекте до актуальных версий<br />

=======================================

## Найденные ошибки логики приложения

1.  файл models/game.js ошибка экспорта<br />
        было: function(sequelize, DataTypes) {<br />
        стало: module.exports = function (sequelize, DataTypes)<br />

1.  ошибка экспорта<br />
    файл db.js стр. 20 добавлен module.exports = { sequelize, DataTypes: Sequelize.DataTypes };<br />

1.  TypeError: db.sync is not a function<br />
    файл **app.js** исправлено строка 9<br />
        ```db.sequelize.sync();```

1.  notNull Violation: user.passwordHash cannot be null<br />
    файл **controllers\usercontroller.js** стр.12 passwordhash => passwordHash

1.  файл **controllers\gamecontroller.js** строка 9<br />
        было function findSuccess(data)<br />
        стало function findSuccess(games)

1.  файл **controllers\gamecontroller.js** строка 76<br />
        было owner_id: req.user<br />
        стало owner_id: req.user.id

=======================================

## Рефактор кода

1.  обозначение переменных **var** заменено на более современные **let** & **const**

1.  добавлены **;** и **,** в конце строк где это необходимо

1.  добавленна деструктуризация где это возможно, например:
<table>
    <tr>
        <td>Было</td>
        <td>Стало</td>
    </tr>
    <tr>
        <td>
            function deleteFail(err) {
                res.status(500).json({
                    error: err.message
                })
            }
        </td>
        <td>
            function deleteFail({ message }) {
                res.status(500).json({ error: message });
            }
        </td>
    </tr>
</table>
