### 身份证校验（react版）
```
class IdNoValidate {
  constructor(props) {
    this.powers = [
      "7",
      "9",
      "10",
      "5",
      "8",
      "4",
      "2",
      "1",
      "6",
      "3",
      "7",
      "9",
      "10",
      "5",
      "8",
      "4",
      "2"
    ]
    this.parityBit = [
      "1",
      "0",
      "X",
      "9",
      "8",
      "7",
      "6",
      "5",
      "4",
      "3",
      "2"
    ]
    this.sex = 'male'
  }

  valid18 = (_id) => {
    _id = _id + "";
    const _num = _id.substr(0, 17);
    const _parityBit = _id.substr(17);
    let _power = 0;
    for (let i = 0; i < 17; i++) {
      //校验每一位的合法性

      if (_num.charAt(i) < '0' || _num.charAt(i) > '9') {
        return false;
        break;
      } else {
        //加权

        _power += parseInt(_num.charAt(i)) * parseInt(this.powers[i]);
        //设置性别

        if (i == 16 && parseInt(_num.charAt(i)) % 2 == 0) {
          this.sex = "female";
        } else {
          this.sex = "male";
        }
      }
    }
    //取模

    const mod = parseInt(_power) % 11;
    if (this.parityBit[mod] == _parityBit) {
      return true;
    }
    return false;
  }

  valid15 = (_id) => {
    _id = _id + "";
    for (let i = 0; i < _id.length; i++) {
      //校验每一位的合法性

      if (_id.charAt(i) < '0' || _id.charAt(i) > '9') {
        return false;
        break;
      }
    }
    const year = _id.substr(6, 2);
    const month = _id.substr(8, 2);
    const day = _id.substr(10, 2);
    const sexBit = _id.substr(14);

    //校验年份位
    if (year < '01' || year > '90')
      return false;

    //校验月份
    if (month < '01' || month > '12')
      return false;

    //校验日
    if (day < '01' || day > '31')
      return false;

    //设置性别
    if (sexBit % 2 == 0) {
      this.sex = "female";
    } else {
      this.sex = "male";
    }
    return true;
  }

}

export default new IdNoValidate()
```
使用时:
15位身份证：`IdNoValidate.valid15(value)`
18位身份证：`IdNoValidate.valid18(value)`
