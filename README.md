# jsonForm


#####usage
```
    //example data
    var data = {
        primitives: {
            number: 12,
            string: "Test string",
            boolean: true,
            arrayOfNumbers: [42, 33, 11],
            arrayOfStrings: ["one", "two", "three"]
        },
        selectMe: "Not",
    };

    /**
    *   jsonForm(HTMLElement container, Object data, [object options])
    **/
    var form = new jsonForm($("body")[0], data, {
        meta: {
            selectMe: {
                type: "select",
                options: ["Not", "Not funny"]
            }
        }
    });
```


#####define custom types
```    
    jsonFormRegisterType("select", function(meta, key, data, parent, path){
       if (!meta.options) {
           console.error("type 'select' needs options");
           return;
       }
       let label = document.createElement('label');
       let span = document.createElement('span');
       span.innerHTML = key;
       let select = document.createElement('select');
       select.dataset.name = key;
       select.dataset.type = 'select';
       select.setAttribute("name", key);
       for (let i = 0; i < meta.options.length; i++) {
           let option = document.createElement('option');
           option.innerHTML = meta.options[i];
           option.setAttribute("value", meta.options[i]);
           select.appendChild(option);
       }
       select.value = data[key];

       label.appendChild(span);
       label.appendChild(select);
       parent.appendChild(label);
   }, function(element) {
       return element.value;
   });
```