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

## 알아야할 내용

1. db.query(sql, params, (콜백함수))
- db.query는 첫번째 인자에서 쿼리문을 보내주고 두번째 인자는 해당하는 params를 세번째 인자는 콜백함수를 보내줍니다. 여기서 두번째 인자는 params를 사용하지 않을경우 생략하면 됩니다.  

2. ?문 (만약 ? 쓰기 싫으면 이터럴 문법으로 해결 가능)
- ?는 쿼리문에서 params의 값을 받아올수 있습니다. 이때 params는 배열에 담을수 있고 ?의 순서에 맞게 넣어 주면 됩니다.  

3. result.insertId
- result.insertId는 insert문이 실행했을때, 삽인된 데이터의 id값을 얻는 방법입니다.