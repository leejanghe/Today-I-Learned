## sprint_short 레퍼런스

```js
const utils = require('../../modules/utils');
const { url: URLModel } = require('../../models');

module.exports = {
  get: async (req, res) => {
    const result = await URLModel.findAll();
    res.status(200).json(result);
  },
  post: (req, res) => {
    const { url } = req.body;

    if (!utils.isValidUrl(url)) {
      return res.sendStatus(400);
    }

    utils.getUrlTitle(url, (err, title) => {
      if (err) {
        console.log(err);
        return res.sendStatus(400);
      }

      URLModel
        .findOrCreate({
          where: {
            url: url
          },
          defaults: {
            title: title
          }
        })
        .then(([result, created]) => {
          if (!created) {
            return res.status(201).json(result); // find
          }
          res.status(201).json(result); // Created
        })
        .catch(error => {
          console.log(error);
          res.sendStatus(500); // Server error
        });
    });
  },
  redirect: (req, res) => {
    URLModel
      .findOne({
        where: {
          id: req.params.id
        }
      })
      .then(result => {
        if (result) {
          return result.update({
            visits: result.visits + 1
          });
        } else {
          res.sendStatus(204);
        }
      })
      .then(result => {
        res.redirect(result.url);
      })
      .catch(error => {
        console.log(error);
        res.sendStatus(500);
      });
  }
}
```

## 두 레퍼런스 비교하기

```js
// controllers/links/index.js
const { getUrlTitle, isValidUrl } = require("../../modules/utils");
const { url: URLModel } = require("../../models");

module.exports = {
  get: async (req, res) => {
    const result = await URLModel.findAll();
    res.status(200).json(result);
  },
  post: async (req, res) => {
    const url = req.body.url;
    if (!isValidUrl(url)) {
      return res.sendStatus(400);
    }
    getUrlTitle(url, async (err, title) => {
      if (err) {
        return res.sendStatus(400);
      }
      try {
        const [result, created] = await URLModel.findOrCreate({
          where: {
            url,
          },
          default: {
            title,
          },
        });
        if (created) {
          return res.status(201).json(result); // 새로 생성된 경우 create
        }
        res.status(201).json(result); // 조회한 경우 find
      } catch (error) {
        console.log(error);
        res.sendStatus(500);
      }
    });
  },
  redirect: async (req, res) => {
    const urlId = req.params.id;
    const result = await URLModel.findOne({
      where: {
        id: urlId,
      },
    });
    if (!result) {
      return res.sendStatus(204); //찾는게 없습니다...
    }
    try {
      await result.update({
        visits: result.visits + 1,
      });
      const redirectUrl = result.url;
      res.redirect(redirectUrl);
    } catch (err) {
      res.sendStatus(500);
    }
  },
};
```