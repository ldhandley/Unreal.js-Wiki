* See also https://github.com/ncsoft/Unreal.js/blob/master/Examples/Content/Scripts/extension-test.js
* Add some `test-xxx.js` on your `Content/Scripts/tests` to register automated test suite.

```
const ops = {TestFlags : 0x02000000 | 0x00000001 | 0x00000002}
describe('Javascript_Test1', opts, function () {
    before(function () {
        console.log('before test1')
    })
    after(function () {
        console.log('after test1')
    })
    it('should fail properly',function () {
        throw new Error("1")
    })
    describe('async', function () {
        before(function () {
            console.log('before inner')
        }) 
        it('should handle time out properly', function (done) {
            setTimeout(function () {
                done()
            },500)            
        })
    }) 
}) 
```

