jQuery(document).ready(function(a) {
    var email = document.querySelector('#billing_email');
    var signup = document.querySelector('#woo_ml_subscribe');
    if (email !== null) {
        email.addEventListener('blur', (event) => {
            if(email.value.length > 0) {
                ml_sub_checkout();
            }
        });
    }

    if (signup !== null) {
        signup.addEventListener('click', (event) => {
            if(email !== null && email.value.length > 0) {
                ml_sub_checkout();
            }
        });
    }

    function ml_sub_checkout() {
        jQuery.ajax({
            url: woo_ml_public_post.ajax_url,
            type: "post",
            data: {
                action: "post_woo_ml_email_cookie",
                email:email.value,
                signup:signup ? signup.checked : false
            }
        })
    }
});