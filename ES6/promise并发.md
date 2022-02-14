# promise并发

* promise.all -->并发请求且都resolve后执行回调，缺点：短路特性,一个请求reject导致整个状态reject
* primise.race -->并发请求有一个resolve后执行回调，缺点：短路特性,一个请求reject导致整个状态reject
* promise.allSettled -->并发请求且都状态完成（或resolve或reject）后执行回调
  ```
  const myPromise = {
    allSettled: function (arr) {
      return new Promise(function (resolve, reject) {
        if (Object.prototype.toString.call(arr) !== '[object Array]') {
          return reject(
            new TypeError(
              typeof arr +
              ' ' +
              arr +
              ' ' +
              ' is not iterable(cannot read property Symbol(Symbol.iterator))'
            )
          );
        }
        let args = Array.prototype.slice.call(arr);
        if (args.length === 0) return resolve([]);
        let arrCount = args.length;
        /**
          * 返回promise
          * @param { int } index promise下标
          * @param { Object } value 返回值
          */
        function resolvePromise (index, value) {
          if (typeof value === 'object') {
            let then = value.then;
            if (typeof then === 'function') {
              then.call(
                value,
                function (val) {
                  args[index] = {
                    status: 'fulfilled',
                    value: val
                  };
                  if (--arrCount === 0) {
                    resolve(args);
                  }
                },
                function (e) {
                  args[index] = {
                    status: 'rejected',
                    reason: e
                  };
                  if (--arrCount === 0) {
                    resolve(args);
                  }
                }
              );
            }
          }
        }
        for (let i = 0; i < args.length; i++) {
          resolvePromise(i, args[i]);
        }
      });
    }
  };
  ```


