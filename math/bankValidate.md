### 银行卡检验算法
```javascript
/**
 * [validate_card_luhn Luhn算法检验卡号]
 *
 * @param  {String} card_number [需要检验的卡号]
 * @return {Boolean}
 *
 * @via https://zh.wikipedia.org/wiki/Luhn%E7%AE%97%E6%B3%95
 */
const BankCardValidate = function (card_number){
    // 卡号字符串化并去除空格，仅保留数字
    let str_digits = (card_number+'').replace(/[\D]/g, '');

    // 银行卡号必须为12-19位数字
    if(!/^\d{12,19}$/.test(str_digits)){
        return false;
    }

    // 根据luhn规则，将卡号数组化，并反转顺序，以便于操作
    let luhn_digits = str_digits.split('').reverse(),
        // 取第1位作为后续的验证号码
        luhn_checkcode = parseInt(luhn_digits.shift(), 10);

    let loop_length = luhn_digits.length,
        loop_index = loop_length;

    let luhn_sum = 0;
    for(; loop_index>0; loop_index--){
        let _i = loop_length-loop_index,
            _k = parseInt(luhn_digits[_i], 10);
        let _add_val = _k;
        // 偶数字段 需要*2，并且大于10的数字要相加2个位数的值
        if((_i%2)===0){
            let _k2 = _k*2;
            switch (_k2) {
                case 10: _add_val = 1; break;
                case 12: _add_val = 3; break;
                case 14: _add_val = 5; break;
                case 16: _add_val = 7; break;
                case 18: _add_val = 9; break;
                default: _add_val = _k2;
            }
        }
        luhn_sum += _add_val;
    }

    /* 方法1
       1. 从校验位开始，从右往左，偶数位乘2，然后将两位数字的个位与十位相加；
       2. 计算所有数字的和（67）；
       3. 乘以9（603）；
       4. 取其个位数字（3），得到校验位。
     */
    let luhn_sum9 = luhn_sum*9,
        luhn_sum9_last_code = parseInt((luhn_sum9+'').replace(/\d+(\d$)/, '$1'), 10);
    return (luhn_sum9_last_code===luhn_checkcode);

    /* 方法2
       1. 从校验位(即不包括该位数)开始，从右往左，偶数位乘2（例如，7*2=14），然后将两位数字的个位与十位相加（例如，10：1+0=1）；
       2. 把得到的数字加在一起；
       3. 将数字的和取模10（本例中得到7），再用10去减（本例中得到3），得到校验位。
     */
    // let luhn_sum_mod10 = luhn_sum%10,
    //     luhn_sum_checkcode = 10 - luhn_sum_mod10;
    // return (luhn_sum_checkcode===luhn_checkcode);

    /* 方法3
       1. 从校验位(即不包括该位数)开始，从右往左，偶数位乘2（例如，7*2=14），然后将两位数字的个位与十位相加（例如，10：1+0=1）；
       2. 把得到的数字加在一起；
       3. 再加上检验位的数值，将结果取模10，如果余数为0，则符合规则。
     */
    // return (((luhn_sum+luhn_checkcode)%10) === 0);
}

export default BankCardValidate
```
