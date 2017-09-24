// Removing Codecanyon frame

if( document.referrer.indexOf('codecanyon') != -1 ){
	top.location = self.location.href;
}

// No Spam

(function(jQuery){

	jQuery.fn.noSpam = function(){

		return this.each(function(){

			if(jQuery(this).html().indexOf('href') == -1){
				var _class = jQuery(this).attr('class');
				var _temp = jQuery(this).html().split(',,');
				var _eadd = _temp[1] + '@' + _temp[0] + '.' + _temp[2];
				var _etxt = _temp[3] ? _temp[3] : _eadd;
				jQuery('<a class="'+_class+'" href="mailto:' + _eadd + '">' + _etxt + '</a>').insertAfter(jQuery(this));
				jQuery(this).remove();
			}
		});
	};
})(jQuery);

// Slider in header function

var sliderInHeader = function(){

	jQuery('[rel^="in-header-"]').each(function(){

		var a = jQuery(this).attr('rel').split('in-header-')[1].split('-')[0];
		var b = jQuery(this).attr('rel').split('in-header-')[1].split('-')[1];

		if( a == b ){
			jQuery('header').css({
				height: 0
			});
		}else{
			jQuery('header').css({
				paddingBottom : jQuery(this).height() * a / b
			});
			jQuery(this).css({
				top : - jQuery(this).height() * a / b,
				marginBottom : - jQuery(this).height() * a / b
			});
		}
	});
};

// Document Ready

jQuery(document).ready(function(){

	// Social Share

	jQuery('#sh').on('click', '.sh-icon', function(e) {

		e.preventDefault();

		var w = 700,
			h = 700,

			x = window.screenLeft || window.screenX,
	    	y = window.screenTop || window.screenY,

	    	l = x + ( jQuery(window).width() - w ) / 2,
	    	t = y + ( jQuery(window).height() - h ) / 2;

	    // opens a centered (relative to the browser) share popup window
	    window.open( jQuery(this).attr('href'), '_blank', 'width='+w+',height='+h+',left='+l+',top='+t);
	});

	// is it a Mobile Device?

	if( !!navigator.userAgent.match(/(iPhone|iPod|iPad|Android|BlackBerry|BB10|webOS|Windows Phone|mobi|tablet|opera mini|nexus 7)/i) ){
		jQuery('body').addClass('mobiledevice');
	}

	jQuery('#mobilemenu select').change(function(){
		var $option = jQuery(this).children(':selected');
		if( $option.data('url') ){
			window.location.href = $option.data('url');
		}
	});

	jQuery('.showonmobile select').each(function(){

		jQuery(this).change(function(){

			document.location.href = jQuery('option:selected', this).val();
		});
	});

	jQuery('#get').appendTo(jQuery('#topmenu .sizer'));

	// Email No Spam

	jQuery('.mapson').noSpam();

	// Adding to window.resize

	jQuery(window).resize(function(){

		sliderInHeader();

		setTimeout(function(){
			sliderInHeader();
		},1500);
	});

	// Calling for the first time

	sliderInHeader();

	// Adding Envato Referrals :)

	jQuery('a').each(function(){
		var url = jQuery(this).attr('href');
		if( typeof url != 'undefined' ){
			if( ( url.indexOf('codecanyon') != -1 || url.indexOf('themeforest') != -1 ) && url.indexOf('?ref=kreatura') == -1 ){
				jQuery(this).attr('href', url+'?ref=kreatura' );
				if( !jQuery(this).attr('target') ){
					jQuery(this).attr('target','_blank');
				}
			}
		}
	});

	// LayerSlider custom functions

	if( typeof layerSliderTransitions != 'undefined' && typeof curSkin != 'undefined' ){

		var curNav = 'hover';

		if(document.location.href.indexOf('skin=') != -1 ){
			curSkin = document.location.href.split('skin=')[1].split('&')[0];
			jQuery('#cur-skin span').text( jQuery('li[rel="'+curSkin+'"]').text() );
		}
		jQuery('li[rel="'+curSkin+'"]').addClass('highlighted');

		if(document.location.href.indexOf('nav=') != -1 ){
			curNav = document.location.href.split('nav=')[1].split('#')[0];
			jQuery('#cur-nav span').text( jQuery('li[rel="'+curNav+'"]').text() );
		}
		jQuery('li[rel="'+curNav+'"]').addClass('highlighted');

		// Creating transition lists

		jQuery('#transition-list ul').append('<li class="list-title">List of the 2D slide transitions <span>(total available: '+layerSliderTransitions.t2d.length+')</span></li>');

		for( var t2d=0; t2d < layerSliderTransitions.t2d.length; t2d++ ){

			if( !layerSliderTransitions.t2d[t2d].selectable ){
				jQuery('#transition-list ul').append('<li class="selectable-list-item" rel="2d:'+(t2d+1)+'">'+ layerSliderTransitions.t2d[t2d].name +'</li>');
			}
		}

		jQuery('#transition-list ul').append('<li class="list-title">List of the 3D slide transitions <span>(total available: '+layerSliderTransitions.t3d.length+')</span></li>');

		for( var t3d=0; t3d < layerSliderTransitions.t3d.length; t3d++ ){

			if( !layerSliderTransitions.t3d[t3d].selectable ){
				jQuery('#transition-list ul').append('<li class="selectable-list-item" rel="3d:'+(t3d+1)+'">'+ layerSliderTransitions.t3d[t3d].name +'</li>');
			}
		}

		// Transition selector

/*
		jQuery('#transition-list').hover(
			function(){
				jQuery('.ls-container').layerSlider('stop');
			},
			function(){
				jQuery('.ls-container').layerSlider('start');
			}
		);
*/

		jQuery('#transition-list .selectable-list-item').each(function(){
			jQuery(this).on('click',function(){
				jQuery('#cur-transition > span').text( jQuery(this).text() );
				window.LSCustomTransition = jQuery(this).attr('rel');
				jQuery('.ls-container').layerSlider('next');
			});
		});

		// Skin selector

		jQuery('#skin-list .selectable-list-item').each(function(){
			jQuery(this).on('click',function(){
				document.location.href = '?skin='+jQuery(this).attr('rel')+'&nav='+curNav;
			});
		});

		// Navigation selector

		jQuery('#nav-list .selectable-list-item').each(function(){
			jQuery(this).on('click',function(){
				document.location.href = '?skin='+curSkin+'&nav='+jQuery(this).attr('rel');
			});
		});

		if( curNav == 'always' ){
			if( curSkin == 'glass' || curSkin == 'defaultskin' || curSkin == 'minimal' ){
				jQuery('#slider-container .sizer').css('padding-bottom','80px');
			}else{
				jQuery('#slider-container .sizer').css('padding-bottom','100px');
			}
		}
	}

	// Append recommender

	jQuery('.version-recommender:first').css({
		display: 'block'
	}).prependTo( jQuery('article:first ') );

	// WeatherSlider weather showcase

	var forcedaytime = 'day';
	var forcewcode = 116;
	var forcecurtemp = 40;
	var forcewindy = 'true';

	var weatherShowcase = function(){

		jQuery('#weather-showcase *').stop().remove();

		jQuery('#weather-showcase').weatherSlider({
			imgPath : 'http://kreaturamedia.com/wp-content/plugins/WeatherSlider/img/',
			locations : ['GEOLOCATION'],
			forcedaytime : forcedaytime,
			forcewcode : forcewcode,
			forcecurtemp : forcecurtemp,
			forcewindy : forcewindy == 'true' ? true : false,
			WWOAPIKey : 'qusqwcarr4hjrkwdw7mprgps',
			enableSearchField : false,
			enableWeatherInfo : false,
			responsive : false
		});
	};

	if( jQuery('#weather-showcase').length ){
		weatherShowcase();
	}

	jQuery('#weather-condition .selectable-list-item').each(function(){
		jQuery(this).click(function(){
			forcewcode = jQuery(this).attr('rel');
			weatherShowcase();
			jQuery('#weather-condition li:first span').text( jQuery(this).text() );
		});
	});

	jQuery('#daytime .selectable-list-item').each(function(){
		jQuery(this).click(function(){
			forcedaytime = jQuery(this).attr('rel');
			weatherShowcase();
			jQuery('#daytime li:first span').text( jQuery(this).text() );
		});
	});

	jQuery('#temperature .selectable-list-item').each(function(){
		jQuery(this).click(function(){
			forcecurtemp = jQuery(this).attr('rel');
			weatherShowcase();
			jQuery('#temperature li:first span').text( jQuery(this).text() );
		});
	});

	jQuery('#wind .selectable-list-item').each(function(){
		jQuery(this).click(function(){
			forcewindy = jQuery(this).attr('rel');
			weatherShowcase();
			jQuery('#wind li:first span').text( jQuery(this).text() );
		});
	});

	// Global hover menu functions

	jQuery('.cur-list-item, .submenu').each(function(){
		jQuery(this).hover(
			function(){

				var $this = jQuery(this);

				if( $this.closest('#topmenu').length ){

					$this.find('.list b').css({
						left: $this.outerWidth() / 2
					});
				}

				$this.find('.list').removeClass('list-fasthide').addClass('list-hovered list-visible');

			},
			function(){
				jQuery(this).find('.list').addClass('list-fasthide').removeClass('list-hovered list-visible');
			}
		);
	});

	jQuery('.selectable-list-item').each(function(){
		jQuery(this).on('click',function(){
			jQuery(this).parent().find('.selectable-list-item').removeClass('highlighted');
			jQuery(this).addClass('highlighted');
		});
	});
});
