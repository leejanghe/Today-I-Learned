## SPRINT _DB_CMARKET


```js
const db = require('../db');

module.exports = {
  orders: {
    get: (userId, callback) => {
      // TODO: 해당 유저가 작성한 모든 주문을 가져오는 함수를 작성하세요
      let sql = `SELECT *, orders.id FROM orders
      INNER JOIN order_items ON orders.id = order_items.order_id
      INNER JOIN items ON items.id = order_items.item_id
      WHERE orders.user_id = ?
      `;

      const param = [userId]

      db.query(sql, param,(err, result)=>{
        callback(err, result);
      })
    },
    post: (userId, orders, totalPrice, callback) => {
      // TODO: 해당 유저의 주문 요청을 데이터베이스에 생성하는 함수를 작성하세요
      const sql = `INSERT INTO orders(user_id, total_price) VALUES (?,?)`;
      const params = [userId, totalPrice]

      db.query(sql,params,(err,result)=>{
        const nextsql = `INSERT INTO order_items(order_id, item_id, order_quantity) VALUES ?`
        const nextparams = orders.map((el)=>[result.insertId, el.itemId, el.quantity])
        db.query(nextsql, [nextparams], callback)
      })
    }
  },
  items: {
    get: (callback) => {
      // TODO: Cmarket의 모든 상품을 가져오는 함수를 작성하세요
      const queryString = `select*from items`
      db.query(queryString,(err, result)=>{
        if(err) callback(err)
        // console.log(result)
        callback(null, result);
      })
    }
  }
};
```