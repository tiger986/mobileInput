## Input width adaptive and mobile end monitor
#### HTML code
```html
<input id="moneyText" type="number" />
```
#### JS code
```javascript
$("#moneyText").focus();

    var textWidth = function(text){
        var sensor = $('<pre>'+ text +'</pre>').css({display: 'none'});
        $('body').append(sensor);
        var width = sensor.width();
        sensor.remove();
        return width;
    };

    //Mobile end monitor input box
    $("#moneyText").bind('input propertychange', function(){
        $(this).val($(this).val().replace(/[^0-9.]+/,''));//type=number is not supported on IOS
        if($(this).val().length > 6){
            var _val = $(this).val().slice(0,6);
            $(this).val(_val);
        }
        $(this).width(textWidth($(this).val() + 10)); //The width of the input is adaptive to the width of the content
        moneyText = $(this).val();
        if(moneyText > 0 && /^(-?\d+)(\.\d{1,2})?$/.test(moneyText)){ //The value entered can not be <=0 and no more than two bits after the decimal point
            $(".free").css("background", "#FF971B");
        }else{
            $(".free").css("background", "grey");
        }
        //console.log(moneyText);
    });


