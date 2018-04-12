// 创建动态form，Post提交订单
function dynamicForm(path, params, method) {
  const form = document.createElement('form')
  form.setAttribute('method', method || 'post')
  form.setAttribute('action', path)
  const fragment = document.createDocumentFragment()

  Object.keys(params).forEach((value) => {
    const input = document.createElement('input')
    input.setAttribute('type', 'hidden')
    input.setAttribute('name', value)
    input.setAttribute('value', params[value])
    fragment.appendChild(input)
  })
  form.appendChild(fragment)
  document.body.appendChild(form)
  form.submit()
  document.body.removeChild(form)
}


