# make-simple-slider-with-jQuery
Tạo Slider đơn giản với html/css/jQuery

### Cấu trúc HTML

<section id="slider">
    <div class="imgList">
        <figure>
            <img src="images/1.jpg">
        </figure>
        <figure>
            <img src="images/2.jpg">
        </figure>
        <figure>
            <img src="images/3.jpg">
        </figure>
        <figure>
            <img src="images/4.jpg">
        </figure>
        <figure>
            <img src="images/5.jpg">
        </figure>
    </div>

    <ul class="navList">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
</section>

### CSS

* {
    padding: 0;
    margin: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

img {
    width: 100%;
    height: auto;
    display: block;
}

/* slider */
#slider {
    width: 100%;
    height: 500px;
    position: relative;
    overflow: hidden;
}

#slider > .imgList,
#slider > .imgList > figure {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    margin: 0;
}

#slider .navList {
    position: absolute;
    bottom: 20px;
    left: 0;
    z-index: 999;
    width: 100%;
    text-align: center;
}

#slider .navList li {
    color: black;
    width: 20px;
    height: 20px;
    line-height: 20px;
    background-color: #fff;
    display: inline-block;
    margin: 6px;
    border-radius: 50%;
    font-size: 12px;
    text-align: center;
    cursor: pointer;
    font-weight: 700;
    box-shadow: 1px 1px 0 rgb(255, 251, 0);
}

#slider .navList li:last-child {
    margin-bottom: 0;
}

#slider .navList li:hover,
#slider .navList li.active {
    background-color: red;
    color: yellow;
}


### Tiến hành viết jQuery cho slider
$(function () {
    //Tao bien index = 0; de lay phan tu dau tien
    var index = 0;

    $('.imgList figure')
        .eq(index)
        .show()
        .siblings()
        .hide()

    $('.navList li')
        .eq(index)
        .addClass('active')
        .siblings()
        .removeClass('active')

    // Tao su kien on click len li
    $('.navList li').on('click', function () {
        // Khoi tao bien target bang voi index cua chinh no khi click
        var target = $(this).index()

        // Neu target bang voi index hien tai thi khong lam gi het
        if (target === index) {
            return false
        }

        // Goi ham change item
        changeItem(target)

    });

    // Khoi tao ham changeView 
    function changeItem(target) {

        // Thuc hien voi imagList
        $('.imgList figure')
            .eq(target)
            .fadeIn(800)
            .end() // Ket thuc va tim index truoc do out di
            .eq(index)
            .fadeOut(800)

        // Thuc hien voi navList
        $('.navList li')
            .eq(target)
            .addClass('active')
            .end() // Ket thuc
            .eq(index)
            .removeClass('active')

        index = target

    }

});
