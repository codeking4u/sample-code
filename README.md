# sample-code
```
/* Function to make wardrobe section droppable */
function main_section_droppable_init() {
   $(document).find(".dropable-main-section").droppable({
         over: function (event, ui) {
            if ($(ui.helper).find(".sections").length) {
               //console.log($(ui.helper).find('.dvSectionCol').css("width"));
               $(ui.helper).css("width", parseInt($(ui.helper).find('.dvSectionCol').css("width")));
               $(ui.helper).css("height", parseInt($(".dropable-main-section").css("height")) - HEIGHT_THRESHOLD);
               $(ui.helper).find('img, p').hide();

               $(ui.helper).addClass('sectionColor');
            }
         },
         start: function (event, ui) {
            $(ui.helper).addClass('section_droppable');
         },
         drop: function (event, ui) {

            $(ui.helper).removeClass('sectionColor');

            var draggedId = ui.draggable.attr('data-section');
            var new_section_id = Math.floor(Math.random() * 100000) + 1;
            var new_comp_id = Math.floor(Math.random() * 100000) + 50;
            window.prev_from_left = $(".dropable-main-section").offset().left;

            var component = $('.sections');
            if (draggedId) {
               /* check if already added */

               window.set_x = $(document).find('.ui-draggable-dragging').eq(0).offset().left - $("#stack-holder").offset().left;
               $('.w-space').hide();

               if (!revert_section_flag) {
                  /* A check to decide whether to add the section to wardrobe or not */
                  make_subsection_droppable();
                  if (('ontouchstart' in document.documentElement)) {
                     $('.dropable-main-section #' + new_section_id).find('.sectn-buttn.sectn-hover-btn').show();
                     $('.dropable-main-section #' + new_section_id).find('.sectn-buttn.sectn-hover-btn').delay(3000).hide(0);
                  }

                  dropable_section(new_section_id);  /* make the dropped section as droppable */
                  mellomvegg_preview();   /* add extra wall as per logic*/
                  getStepTotals();;  /* generate cost*/

               }
            }
         });
   }
```
