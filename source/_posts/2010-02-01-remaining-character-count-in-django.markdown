--- 
layout: post
title: Remaining character count in django admin
wordpress_url: http://beta.timbroder.com/2010/02/01/remaining-character-count-in-django-admin/
date: 2010-02-01 19:28:00 -05:00
comments: true
tags: []

---
Want to display the remaining characters on a text field in admin? (based off of maxlength or an override) <br />
<br />
``` python
#have your ModelAdmin inherit this to use
class CounterAdmin(admin.ModelAdmin):
    counted_fields = ()
    
    #really for textareas
    max_lengths = {'abstract': 400,}
    
    class Media:
        js = ('js/jquery.js',
              'js/jquery.charCount.js',)
        
    def formfield_for_dbfield(self, db_field, **kwargs):
        field = super(CounterAdmin, self).formfield_for_dbfield(db_field, **kwargs)
        print db_field.name
        print self.counted_fields
        if db_field.name in self.counted_fields:
            try:
                len = self.max_lengths[db_field.name]
                field.widget.attrs['maxlength'] = len
            except: pass
            field.widget.attrs['class'] = 'counted ' + field.widget.attrs.get('class','')
        return field


"""
jquery,charCount.js

/*
 *  Character Count Plugin - jQuery plugin
 *  Dynamic character count for text areas and input fields
 * written by Alen Grakalic 
 * http://cssglobe.com/post/7161/jquery-plugin-simplest-twitterlike-dynamic-character-count-for-textareas
 *
 * Copyright (c) 2009 Alen Grakalic (http://cssglobe.com)
 * Dual licensed under the MIT (MIT-LICENSE.txt)
 * and GPL (GPL-LICENSE.txt) licenses.
 *
 * Built for jQuery library
 * http://jquery.com
 *
 */

/*
 * Modified 2010 Tim Broder for django-admin-charcount
 * http://gpowered.net
 */
 
(function($) {
 $.fn.charCount = function(options){
  // default configuration properties
  var defaults = { 
   allowed: 140,  
   warning: 20,
   css: 'help',
   counterElement: 'p',
   cssWarning: 'warning',
   cssExceeded: 'exceeded',
   counterText: ''
  }; 
   
  var options = $.extend(defaults, options); 
  
  function calculate(obj){
   var count = $(obj).val().length;
   var available = options.allowed - count;
   if(available < = options.warning && available >= 0){
    $(obj).next().addClass(options.cssWarning);
   } else {
    $(obj).next().removeClass(options.cssWarning);
   }
   if(available < 0){
    $(obj).next().addClass(options.cssExceeded);
   } else {
    $(obj).next().removeClass(options.cssExceeded);
   }
   $(obj).next().html(options.counterText + available);
  };

  this.each(function() {     

   $(this).after('<'+ options.counterElement +' class="' + options.css + '">'+ options.counterText +'');
   calculate(this);
   $(this).keyup(function(){calculate(this); });
   $(this).change(function(){calculate(this)});
  });
   
 };

})(jQuery);

/*function init_counters(selector, len){
 $(selector).each(function() {
  //console.log($(this).attr('maxlength'));
  if(len==null){
   len = $(this).attr('maxlength');
  }
  $(this).charCount({
   counterText: 'Characters Remaining: ',
   allowed: len,
  });
 });
}*/

$(document).ready(function(){
 $(".counted").each(function(){
  console.log($(this));
  len = $(this).attr('maxlength');
  $(this).charCount({
   counterText: 'Characters Remaining: ',
   allowed: len,
  });
 });
 //init_counters("input[maxlength]", 80);
 //init_counters("textarea[maxlength]");
 //init_counters("#id_abstract", 400);
});

/*
 * <style type="text/css">
form .counter{
 }
form .warning{color:#600;} 
form .exceeded{color:#e00;}
</style>
*/
"""

``` 
