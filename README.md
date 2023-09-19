# popup


<style>
.popup.grid {
background-image: url({{ 'popup-bg.jpg' | asset_img_url: 'original' }});
background-repeat: no-repeat;
background-size: cover; 
}
</style>


<div class="popup-btn">
<!-- Change the text below to what you need it to be -->
</div>
<div class="popup-overlay" data-lazyload="Anything you want to lazyload">
<div class="popup grid">
  <div class="img-popup">
    <img src="{{ settings.image | img_url : 'original' }}">
  </div>
  <div class="pop-content">
   <div class="footer-block__newsletter">
     <h2 class="footer-block__headin">{{settings.popup_heading}}</h2>
     <p class="news-sub-heading">{{settings.popup_sub_heading}}</p>
            {%- form 'customer', id: 'ContactFooter', class: 'footer__newsletter newsletter-form' -%}
              <input type="hidden" name="contact[tags]" value="newsletter">
              <div class="newsletter-form__field-wrapper">
                <div class="field">
                  <input
                    id="NewsletterForm--{{ section.id }}"
                    type="email"
                    name="contact[email]"
                    class="field__input"
                    value="{{ form.email }}"
                    aria-required="true"
                    autocorrect="off"
                    autocapitalize="off"
                    autocomplete="email"
                    {% if form.errors %}
                      autofocus
                      aria-invalid="true"
                      aria-describedby="ContactFooter-error"
                    {% elsif form.posted_successfully? %}
                      aria-describedby="ContactFooter-success"
                    {% endif %}
                    placeholder="{{ 'Enter Email Address Here' }}"
                    required
                  >
                  <label class="field__label" for="NewsletterForm--{{ section.id }}">
                    {{ 'Enter Email Address Here' }}
                  </label>
                  <button type="submit" class="newsletter-form__button field__button" name="commit" id="Subscribe" aria-label="{{ 'newsletter.button_label' | t }}">
                  SEND
                  </button>
                </div>
                {%- if form.errors -%}
                  <small class="newsletter-form__message form__message" id="ContactFooter-error">{% render 'icon-error' %}{{ form.errors.translated_fields['email'] | capitalize }} {{ form.errors.messages['email'] }}</small>
                {%- endif -%}
              </div>
              {%- if form.posted_successfully? -%}
                <h3 class="newsletter-form__message newsletter-form__message--success form__message" id="ContactFooter-success" tabindex="-1" autofocus>{% render 'icon-success' %}{{ 'newsletter.success' | t }}</h3>
              {%- endif -%}
            {%- endform -%}
          </div>

<span class="popup-close"></span>
</div>

</div>
</div>

 <script>
      $(document).ready(function(){
        setTimeout(function(){

          var check_popuop = localStorage.getItem("popup-btn");

          if(check_popuop != 'cookie-show'){
            
            $(".popup-btn").trigger("click");

            localStorage.setItem("popup-btn", "cookie-show");
          }
          
       },3000);    
        //alert("hello");
      
      });
    </script>

<script>
  document.querySelector(".popup-btn").addEventListener('click', function (e) {
e.stopPropagation();
document.querySelector(".popup").style.display = 'flex';
}, false);
document.querySelector(".popup-btn").addEventListener('click', function () {
document.querySelector(".popup-overlay").style.display = 'flex';
}, false);
document.querySelector(".popup-close").addEventListener('click', function () {
document.querySelector(".popup").style.display = 'none';
document.querySelector(".popup-overlay").style.display = 'none';
}, false);
document.querySelector("body").addEventListener('click', function () {
document.querySelector(".popup").style.display = 'none';
document.querySelector(".popup-overlay").style.display = 'none';
}, false);
document.querySelector(".popup").addEventListener('click', function (e) {
e.stopPropagation();
}, false);
</script>
<style>
.popup {
background-color: #fff;
border-radius: 8px;
padding: 50px 30px;
box-shadow: rgba(0, 0, 0, 0.24) 0px 1px 3px;
position: absolute;
z-index: 25;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
max-width: 800px !important;
height: 400px;
display: none;
width: 100%;
}
@media only screen and (max-width: 767px) {
.popup {
padding: 35px 15px;
}
}
.popup-close:after {
width: 30px;
content: '╳';
position: fixed;
right: 10px;
top: 10px;
font-size: 20px;
line-height: 30px;
cursor: pointer;
}
.popup-btn {
cursor: pointer;
}
.popup-overlay {
position: fixed;
height: 100%;
width: 100% !important;
top: 0;
right: 0;
bottom: 0;
left: 0;
background: rgba(0, 0, 0, 0.6);
display: none;
z-index: 100;
}
 </style>
  {% if template == 'index' %}
 {% render 'newsletter-popup' %}
  {%- endif -%}
 {
    "name": "popup",
    "settings": [
      {
        "type": "image_picker",
        "id": "image",
        "label": "Background Image"
      },
      {
        "type": "text",
        "id": "popup_heading",
        "default": "SIGN UP FOR OUR EMAIL AND GET <SPAN>10%<\/SPAN> OFF ON YOUR FIRST ORDER.",
        "label": "Popup Heading"
      },
      {
        "type": "text",
        "id": "popup_sub_heading",
        "default": "we'll update you with the newest arrivals & sales!",
        "label": "Popup Sub Heading"
      }
    ]
  }

