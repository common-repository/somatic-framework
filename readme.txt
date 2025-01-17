=== Somatic Framework ===
Contributors: somatic
Tags: CMS, custom post type, metabox, custom taxonomy
Donate link: http://somaticstudios.com/code
Requires at least: 4.0
Tested up to: 5.6
Stable tag: 1.8.14
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Adds useful classes for getting the most out of Wordpress' advanced CMS features

== Description ==

This framework is a collection of classes and functions for handling advanced custom post types cases. With just a few defined arrays, it can create custom post types, taxonomies, their labels, menus, metaboxes, and save routines.

NOTE: this began life as an internal development tool, and as such, does not have much (if any documentation) just yet. It's not really end-user friendly in its current state. So if you're not running a site I have built for you personally, you probably don't need it ;-)

== Installation ==

Upload, activate, have a drink... but first, install and activate Scribu's excellent Posts 2 Posts plugin, which this framework requires!

== Frequently Asked Questions ==

= Do I need this plugin? =

If you're using a theme or setting up a site I built for you, then very likely, yes...

= I updated my call to soma_init_taxonomy() and added new terms, but why aren't they appearing? =

deactivate and reactivate your theme/plugin that contains the function call, as term generation only happens upon activation...

== Changelog ==

= 1.8.14 =
* colorbox update to fix JS errors

= 1.8.13 =
* tweaks for PHP 7.2 compatibility
* changed parsing and storage of user-provided URLS for media to protocol-relative URL, to avoid mixed HTTP/HTTPS issues

= 1.8.12 =
* no longer using custom menu icons, but the built-in dashicons set, so the custom post type argument "icon_set" is deprecated. Simply provide the argument "menu_icon" in the post type declaration. Documentation https://developer.wordpress.org/resource/dashicons/
* removed hacks for injecting custom post type archives into the Nav Menu editor (not needed anymore, and was breaking editor)

= 1.8.11 =
* FIX: parse_query action hook repaired, had stopped working oddly
* added demographics tracking line to google analytics code
* NEW: option to enable built-in page excerpts
* NEW: option to disable attachment pages (redirecting to parent post)
* NEW: option to prevent WP from automatically titling new image uploads with the filename
* more metabox disabling for themeblvd stuff

= 1.8.10 =
* NEW: metabox button "save-back" outputs a save button which immediately redirects back to referring page after saving
* FIX: upload boxes work again with the new plUpload 2.1 that is bundled with wordpress 3.9

= 1.8.9 =
* NEW: api functions soma_queue_notice() and soma_completion_notice(). stores and displays admin notices in the core wp "message box" format.
* FIX: saving framework options from the advanced tab was clearing all options. now all such options are on the same tab. renamed declarations tab > reports
* cleaned up various css issues with metabox attachment items
* added "uploaded X ago" to file attachment display
* added google analytics tracking ID option field and javascript code output

= 1.8.8 =
* NEW: action hook soma_metabox_data_init, provides better location to hook all usage of soma_metabox_data() when declaring metabox field arrays. * soma_metabox_data_init passes $post as an argument, so can finally use functions to provide data to field arguments!
* NOTE: you should never use "admin_init" as the hook for soma_metabox_data() anymore. Fires too early, no $post data possible
* NEW: field type "button", outputs clicker buttons in the field row, can pass label and URL (or show a submit button)
* audio shortcodes in fields now include ID of the attachment for more data than just the file src
* radio field types now show emphasis on the selected radio label

= 1.8.7 =
* NEW: option field for TypeKit ID, sets up javascript for you
* FIX: finally solved the issue with post titles and slugs not getting saved when custom post type doesn't "support" title
* FIX: deleting content from core data fields actually clears the saved field now
* when using custom post title fields (not wp's title field), and field is left blank, title is changed to "Untitled"
* new CPT icons
* NEW: filter for custom metabox field data, "soma_field_data_[id]". Allows manipulation of $meta right before fields get rendered
* readonly field type text gets run thru the_content filter, so formatting actually works

= 1.8.6 =
* Multi-Site support. Activation hook accomodates network-wide scenario.
* fully private site option. forces login on front-end to view anything at all.
* disable RSS feeds option
* NEW: filter 'soma_js_vars' allows changes/additions to the variables passed to javascript
* NEW: when debug active, current template path is shown in admin bar

= 1.8.5 =
* NEW: somaRequest class and soma_request_[*] dynamic action hook -- works much like wp_ajax_ hooks, but without the ajax. Triggered with the 'soma_request' query_var or as simple URL query params via $_GET. Very handy for export/download functions to fire without leaving current page!
* NEW: somaFunctions::build_request_link() creates link to trigger soma_request_[*] action hook and pass along data (string or array)
* all functionality of the old somaDownload class is now incorporated in an soma_request_legacy-download action hook (though the old "download" query var remains for backwards compatibility)

= 1.8.4 =
* NEW: api function soma_fetch_file() returns bunch of really handy info about an attachment's file, including download link
* swapped order of params on soma_select_number_generator() to make including 'zero' second

= 1.8.3 =
* NEW: custom post type icons integrated - can now be picked with the arg "icon_set" (makes it easier to place soma-config.php in mu-plugins folder, as no additional images have to be included)
* CHANGE: soma_init_type arg "icons" is now "custom_icon_path", to differentiate from built-in icon sets (all old configs will need to be updated, or use the new integrated sets)
* gallery field items now show less attachment meta fields for filetypes other than images
* sanitizing form field values less, allowing for decimals
* better handling of mime-type file icons

= 1.8.2 =
* FIX: action and filter hooks in somaSave class with same name resulted in nuked data upon save
* NEW: filter hook to construct save data in special field cases: "soma_field_new_save_data"
* FIX: finally cracked the issue of custom fields saving core column data and dealing with the quirks of tinymce ID limitations
* cleaned up undefined indexes and variables

= 1.8.1 =
* FIX: severe bug that prevented saving any changes from a wp_editor() richtext field or core post data columns
* NOTE: when you spawn a richtext or html field type, the ID you give should only consist of lowercase letters, nothing else. A function has been included to provide backwards compatibility with older configs where underscores or dashes were used in the ID.

= 1.8 =
* FIX: finally using wp_update_post() instead of $wpdb->update for core data, so now text gets sanitized and filtered as normal before saving.
* FIX: major bugs in metabox text saving, resulting in escaped backslash quotes and more issues.
* FIX: safe ID's now generated when using wp_editor(), as it's pretty fussy about ID's. You can use anything you want now without setting it off
* FIX: finally isolated saving of core metabox data types thru custom ID's, so they don't get hijacked by core save routines

= 1.7.10 =
* NEW: gallery field of attachments now supports editing of each attachment's title, caption, description and changing sort order!
* FIX: colorbox overlays in admin have maxheight and maxwidth set
* FIX: soma-public-jquery.js was failing and halting js when front-end colorbox was not enabled
* NEW: sort_group_type -> ancestors allows Sort Order page via post_parent grouping (only deals with top-level parents)
* FIX: saving post_title fields now also updates the post slug to match
* FIX: more accurate use of wp_localize_script

= 1.7.9 =
* FIX: soma_fetch_image was failing to return image sizes if none were generated because original was too small

= 1.7.8 =
* FIX: errors using wp_register_style
* FIX: broken styling of save-changes buttons
* UPDATE: jquery UI smoothness theme updated to 1.9.2, removed local jQuery UI datepicker, as it's in wp-core
* UPDATE: jquery UI timepicker addon to 1.2.1
* NOTE: for 'upload-files' field types, the ID string for that field cannot contain a dash, or it breaks plupload js
* added more filetype icons
* metabox css tweaks
* finally defined default args for metabox data and field arrays
* more undefined index cleanup...
* NEW: each metabox field can have "restrict" parameter to hide from non-staff level users
* FIX: metabox jquery errors
* started moving soma_metabox_generator() to be useful outside of post editor
* modified soma_plupload.js to be useful outside of the post editor
* metabox field data type "user" is gone. Use "core" instead and "post_author" as the field ID
* metabox select fields now don't consider 0 to be "empty" if referring to post_parent
* framework option for enabling Colorbox on front-end posts now automatically makes image links lightboxed
* page-attributes metabox is no longer forced to show when post type is hierarchical (might want to use custom fields instead)
* FIX: soma_singular_term() parameters fixed, can also fetch term_id
* NEW: metabox field type "radio-horizontal" displays radio buttons... horizontally
* NEW: can specify (per customposttype args or via post_meta key) "delete_attachments_upon_deletion" - to have all media attachments (and their files) specifically attached to a post deleted when that post gets deleted. I call it the "ritual suicide" option...

= 1.7.7 =
* NEW action hook: soma_init - allows hooking init but only after Somatic Framework loads. Otherwise other plugins trying to register custom types would fail if they loaded before this one.
* FIX: major bug with hierarchical post types not supporting anything
* NEW functions fetch_sub_pages() and fetch_root_pages() for dealing with hierarchical post types
* fixed stray undefined indexes...
* FIX: deep bug that caused hierarchical CPTs to return 404 on child pages

= 1.7.6 =
* NEW: option to enable custom link redirects via /go/[slug]. Use the filter 'soma_go_redirect_codes' to add a new slug/url pair. remember to flush rewrite rules
* NEW: api soma_go_link(), returns HTML link code for an existing go code and link text
* NEW: system for dynamically showing/hiding certain metabox field rows based on a list selection
* field argument 'reveal-control' - should be assigned only to a 'radio' or 'select' field type (and only one per page)
* field argument 'reveal-group' - array of names corresponding with the possible values of the reveal-control selector. If the current value is in the array, that field is shown, otherwise hidden
* changes to table structure for metabox field rows - now descriptions and extra options are all within the main field row, so they can all be hidden together
* FIX: taxonomy dropdown selectors can finally use "Create New" and have a new term created upon save! just use soma_select_taxonomy_terms('mytaxonomy', true) to generate the field 'options' array

= 1.7.5 =
* FIX: metabox field type 'checkbox-single' (now known as 'toggle') finally works as expected! You can uncheck things now :-P
* NEW: soma_fetch_image(), soma_asset_meta(), soma_attachments(), soma_fetch_image(), soma_singular_term() now accept either a post object or post ID (integer or string)
* improved the save hooks to fire only when dealing with our custom fields
* thumbnail columns now automatically adjust width according to thumbnail options (max width 200px)
* FIX: finally overhauled somaSave and somaMetaboxes classes to more accurately handle saving and retrieving multiple items vs. single items
* NOTE: when checkboxes are desired (one or more), use the new field type "checkbox" and pass options array. the old 'checkbox-single' type is deprecated in favor of 'toggle' - but to be used only with meta data (not taxonomy, etc)

= 1.7.4 =
* NEW api soma_attachments(), wrapper for get_posts() returns array of attached post objects, minus the featured image (unless specified)
* NEW api soma_fetch_image(), basically just renamed soma_featured_image() [still around for backwards compatibility] - reflects its ability to retrieve image data for any attachment, not just featured images
* somaFunctions::fetch_attached_media() now takes mime-type argument and an optional argument to exclude the featured image
* metabox field type "attachment" is now "gallery" (still with data of "attachment"). Shows all attached images or audio or video (via mediaelement)
* metabox "gallery" field type now excludes the featured image automatically, allowing fully independent featured image and gallery attachment uploaders
* metabox field argument for data of "attachment" can also include "mime-type" for filtering retrieved attachments by media type
* NOTE: metabox field "upload-images" has been folded into "upload-files", which has abandoned the old html file selector input model, and now uses the hot new plUpload system.
* NEW: metabox field "upload-files" can now handle audio as well as images!
* old field type for featured image plUpload boxes, "upload-featured", is now deprecated: use "upload-files", with 'data' arg set to "featured"
* FIX: multiple plUpload boxes on the same page now behave!
* FIX: soma_fetch_image() was failing certain specific requests, now returns original full file URL if the requested size is not available (eg: original pic was smaller than site's "large" setting)
* FIX: soma_fetch_image() now includes custom image sizes when available
* NEW: soma_fetch_image() now returns title, description, caption, and alt text
* NOTE: this means the key for the thumbnail image is now "thumbnail" (as returned by wp), and not "thumb", as it had been hardcoded before. Your old calls to soma_featured_image() for thumbs are likely broken now
* NOTE: the missing image placeholder is now one single size image, so make sure you manually indicate the width and height in your image tags (or else they'll all display at 512px)
* options to hide new Thesis 2.0 metaboxes
* cleaned up all undefined index warnings
* FIX: custom post type update messages were not being produced properly...
* FIX: media uploader metabox field type works again
* improvements to the styling and behavior of the sorting pages
* improvements to the somaUploadField class
* NOTE: any old metabox fields dealing with attachments should probably be revisited...

= 1.7.3 =
* FIX save routines on external media and images don't die anymore if empty
* NEW metabox field: "link"
* metabox CSS tweaks
* cleaned up some deprecated junk in manage_posts_columns calls
* NEW api function soma_get_excerpt() for fetching existing post_excerpt or manually creating one from post_content via post ID or object
* fixed warning with lack of metabox definitions. Now, in soma_init_type args, you can declare blank_slate = true to remove all core wp metaboxes (in effect, declaring no post_type_support for title, editor, author, etc.). This replaces the old behavior of passing an empty array to the "supports" arg, which didn't work well when parsing default args. It also means the missing metabox warning will *only* appear if the post type doesn't support any core wp boxes.

= 1.7.2 =
* FIX default behavior to not always show the toolbar on the front end [facepalm]
* NEW users have toolbar off by default
* NEW option to force toolbar to show for everyone, everywhere
* NEW soma_option for setting the Login page logo
* custom login logos should be transparent PNG of 320x70 exactly, with content aligned bottom center for best results
* stopped hiding user profile fields
* now using transients with soma_set_option(), allowing caching, reducing DB load when calling soma_set_option() on every page load
* option to force admin bar only applies to logged in users
* $_GET and $_POST are now passed to JS via soma_vars

= 1.7.1 =
* fixed stripslashes problem with quotes in text fields
* kint debug aborts if output buffering not on
* login page indicator if WPEngine

= 1.7 =
* NEW image uploader metabox field type. Uses WP included plUpload for drag-n-drop, queued uploads, creates attachments upon saving. Can also be used for featured images.
* new option to disable screen options tab

= 1.6.9 =
* disabled privileges check in save_asset() that conflicted with paypal digital goods checkout
* fixed bug that output junk to the login screen
* fixed column listing error when no columns are defined in a CPT
* changed save_asset() to not fire when quickedit is used
* changed save_asset() to not wipe out our custom defined metadata and taxonomies when other forms/plugins call save_post
* fixed problem where quickedit would fail to complete because of jQuery error (when custom columns were in use) - NOTE: after quickedit save updates, it won't show the custom columns - refresh the list page to see custom columns again

= 1.6.8 =
* removed hook that fired on user profile update, as it got stuck in a fatal infinite loop with any other plugin that tried to update a user...
* changed SOMA_URL constant (and all others built on it) to use https:// scheme when in use

= 1.6.7 =
* fixed error in disabling paging for custom taxonomies defined elsewhere...
* updated placeholder images
* added flag to custom post type definitions to identify which CPT's have been defined through this framework
* Admin CSS improvements

= 1.6.6 =
* FIX: removed undefined metabox errors for built-in post types
* NOTE: for soma_debug output, php.ini must be configured with "output_buffering" set to ON (not a number like 4096), or you will see a bunch of "Cannot modify header information" warnings coming from Kint....
* NEW: option to enable Colorbox JS on front-end
* metabox field save button can now be set to always change post status to "publish"
* FIX: fatal SQL error in the posts_orderby filter when order_by wasn't defined (default was set to date instead of post_date)
* NOTE: when defining sort_by values for CPT's, do not use the WP_Query values for 'orderby' - must use actual wp_posts column names (like post_title instead of just title)

= 1.6.5 =
* NEW: soma_init_type() arguments "sort_by" (post_date, post_title, post_author, menu_order, meta_value) and "sort_order" (asc, desc) to override the default query filters
* REMOVED: soma_init_type() argument "sortable" is gone - replace with new "sort_by"
* NOTE: must modify all calls to soma_init_type()!
* moved all filtering of parse_query into somaTypes class
* fixed various "missing index" errors
* CHANGE: soma_select_items() second argument is now an array of any arguments you would pass to get_posts()

= 1.6.4 =
* soma_featured_image now handles custom image size labels (from add_image_size) via the $specific argument
* new metabox field: p2p-select - allows assigning single p2p relationship via dropdown (warning: must hide the core p2p admin box if you use these fields! there's a conflict in the save routines)
* new metabox field: p2p-multi - allows assigning multiple p2p relationships via checkboxes
* can now use soma_metabox_data() with core post and page types
* updated jqueryUI timepicker to 0.9.9
* timepicker metabox type now actually works...

= 1.6.3 =
* new Sort Order grouping: p2p, give it a P2P connection type name (ex: sortable = true, sort_group_type = p2p, sort_group_slug = albums-tracks)
* new save action hook: soma_save_asset
* admin css tweaks
* metabox field type p2p-thumbs is now p2p-objects

= 1.6.2 =
* expanded list of metaboxes to disable to include core WP ones
* new ability to specify grouping of cpt objects on the Sort Order page, if sorting is enabled (ex: sortable = true, sort_group_type = taxonomy, sort_group_slug = genres)
* fixed css bug in clicker buttons
* fixed query parsing on sortable post types - now the query is always filtered to sort the query output by menu_order ASC (as was intended) - so now admin and front-end post listings reflect the proper order!
* new option to disable paging (list all items instead) per post type
* moved all custom somatic framework arguments for register_post_type within the core arguments array, so they're stored as part of the post type object and can be retrieved with get_queried_object()
* NOTE: make sure you've updated any calls to soma_init_type, so that the "sortable", "create_nav_item", etc args are passed in the main "args" array!

= 1.6.1 =
* disabling admin menus also gets rid of the +New admin bar item
* using checked() on html forms now
* better handling of missing metabox config data...
* tabs on the option page
* subtle tweaks to login page
* using wp_enqueue_scripts() globally now
* favicon set and display on options page
* options page is now top-level, with subpages
* import/export of framework options
* fixed menu detection with soma_init_type argument "create_nav_item"
* custom post types and taxonomies now actually display list metaboxes in Appearance->Menus if "show_in_nav_menus" arg is true (rather than simply being available to show via Screen Options, but unchecked by default)

= 1.6 =
* NEW somatic_framework_options settings container (serialized array of default options)
* NEW api function: soma_set_option() - allows easy manipulation of somatic_framework_options in wp_options table
* NEW global var: $soma_options - quick checking of current options with DB query
* NEW settings page to toggle debug mode, plugin dependencies, dashboard widgets, bottom admin bar, editor metaboxes, admin menus, and more
* NEW daily cron task, use action hook 'soma_daily_event'
* NEW csv export class, included in trunk but not ready for prime time
* NEW plugin checks for minimum wordpress version, aborts otherwise...
* NEW for CPT's with show_in_nav_menu = true, an item will be available at the top of the "view all" tab in the CPT panel of Appearance->Menus. Adding that to the menu will create a custom nav menu item configured to display CPT archives
* NEW arg 'create_nav_item' for soma_init_type() - replaces the 'navbar' arg
* CHANGE: custom post type nav items - instead of filtering the nav menu output and tacking our CPT's on, we're actually creating real nav menu items in the DB. Then you can go to Appearance->Menus and re-order that item like any other
* REMOVED filter: soma_custom_type_nav_position, as the CPT nav items aren't being generated by somaTypes::custom_type_nav() anymore
* DEPRECATED: old options soma_meta_prefix, soma_meta_serialize, soma_debug - store your values in the new somatic_framework_options settings container. ex: update_option('somatic_framework_options', array('meta_prefix', '_foo'));
* CHANGE: keycommand for showing/hiding the debug bar panels is now "\" for minimized and alt+"\" for maximized view
* sexy settings link right on the plugins page!
* improved the example php config templates
* better handling of missing metabox config data in add_boxes()
* independent handling of current nav menu item classes with fix_nav_classes()

= 1.5.1 =
* fixed fatal error in checking for Kint when debug mode is enabled...

= 1.5 =
* included the awesome Kint PHP debugger v.32 (http://code.google.com/p/kint/)
* integration with the Debug Bar plugin for maximum awesomeness (http://wordpress.org/extend/plugins/debug-bar/)
* when Debug Bar is installed, hit the ";" or "'" keys to toggle the debug panel in maximized or partial view
* NEW API function: soma_dump() - outputs data to screen (or to the Debug Bar panel, much nicer!)
* re-enabled admin bar on front-end (had been disabled globally, overriding user options)
* NEW option: soma_debug - controls inclusion of Kint classes, Debug Bar hooks, and various debugging things. Defaults to off.
* NEW js and css for injection on the public side of wordpress
* cleaned up all PHP Notice warnings! go ahead and turn on WP_DEBUG...

= 1.4.4 =
* corrected critical bug introduced by 1.4.3 fixes - save routines now work again...

= 1.4.3 =
* fixed unnecessary suicide when trying to save a post/page if no custom metabox definitions exist yet...
* now fully compliant with WP guidelines! ;-)

= 1.4.2 =
* fixed unreliable usage of isset() for array keys in soma_init_type. Wasn't registering user parameters for navbar and sortable properly [facepalm]
* NEW somaFunctions::is_blank() for checking whether variable/array key is actually blank or just set to "0" or false

= 1.4.1 =
* soma_external_media() now supports SoundCloud URLs!
* fixed inconsistencies with metabox handling of media types. Make sure data=attachment and type=media
* fixed problem with external media metabox colorbox iframes (no dimensions were given)
* fixed colorbox trigger play icon to be more reliable
* mediaelement.js replaces jPlayer when displaying media attachments in admin metaboxes (though at the moment requires wp plugin http://wordpress.org/extend/plugins/media-element-html5-video-and-audio-player/)

= 1.4 =
* NEW metabox field type: external_media - Text field that accepts vimeo or youtube URLs, and fetches that video's metadata via each site's public API. Also saves that response in post_meta for quicker retrieval.
* NEW metabox field type: external_image - Text field that accepts image URL, and can import the image as an attachment, also setting imported image as Featured Image
* NEW API function: soma_external_media() - parses URL from either youtube or vimeo, returns an array with basic metadata, including ID, title, thumbnails - optionally imports source image to local library and sets the post_thumbnail!. NOTE: desired video must not be private, password-protected, or have embedding disabled by the owner!
* NEW internal function: somaFunctions::attach_external_image() - sideloads an external image URL into the wordpress media library and attaches to a post
* updated colorbox.js to 1.3.19
* fixed broken url for jquery UI smoothness css
* fixed link output in custom_type_nav() for when the custom post type slug includes variables for taxonomy permalinks
* NEW filter: soma_custom_type_nav_position, for determining with the nav items that are automatically generated for custom post types are placed before or after the existing menu items. Defaults to "after" (return "before" via filter to change)
* fixed soma_init_type ignoring navbar=false and inserting menu item anyway
* fixed broken css on Sort Order pages
* consolidated metabox description row code (too much duplication)
* a smattering of other tweaks, enhancements, and bugfixes..

= 1.3.2 =
* admin footer text output
* fixed numeric field input to allow colon (:)

= 1.3.1 =
* fixed problem with setting the option soma_meta_serialize, which needs to be passed 0 or 1, not boolean true or false (false resulted in empty option_value, which broke everything)
* NOTE: when using soma_asset_meta(), don't include the prefix when specifying the post_meta key! it gets added automatically. Just use the exact ID you gave when declaring the field in  soma_metabox_data()
* NEW API function: soma_singular_term() for retrieving the term of a taxonomy that is meant to have only one value at a time.
* NEW documentation - example PHP code in the doc folder, to help demonstrate how to use the somatic framework

= 1.3 =
* added 'navbar' argument to soma_init_type to choose whether to display a nav menu item to the primary navbar for custom post types [default: true]
* added 'sortable' argument to soma_init_type to choose whether to make items manually sortable (instead of automatically sorting by date) [default: false]
* post meta keys are now stored individually by default. If you want to store all metadata per post as a serialized array in a single key, you need to set the option 'soma_meta_serialize' to true
* the default post meta key name prefix is "_soma" (what you give as the ID for a metabox field is added to it). If you want a custom prefix, you need to set the option 'soma_meta_prefix' to "_YOUR_PREFIX"
* admin type sorting page rows fit content better
* NEW API function: soma_asset_meta() for manipulating post_meta (abstracts the core functions to better handle serialization cases)
* NEW API function: soma_featured_image() for retrieving everything you could possibly need to know about the featured image (post thumbnail)
* in edit listing columns, the checkbox column is always included now, so don't need to pass it in soma_init_type column array
* fixed a query parsing filter that was forcing everything to order by menu_order ASC, no matter what...
* had forgotten to actually enqueue jquery UI datepicker and slider js and css this whole time <facepalm>
* added button to clear date values when using datepicker

= 1.2.1 =
* revised somaFunctions::fetch_connected_items() to handle p2p plugin evolution
* note: must pass the p2p type ID and *not* the post_type anymore! Please revise all calls to fetch_connected_items()!
* When passing "p2p" field data with soma_metabox_data(), you must also pass "p2pname" for the unique registered p2p connection ID and "type" (p2p-list or p2p-thumb) for output
* cleaned up save routines, stripslashes bugs
* metabox type "richtext" now uses the new WP3.3 wp_editor() function (multiple rich editors possible, yay!)
* NEW metabox type "html" uses the new WP3.3 wp_editor() function, but without the visual editor
* metabox type "editor" removed - use "richtext" instead with ID of "post_content" and data of "core" if you're trying to replace the core post editor (just make sure to NOT include "editor" in the post type support!)
* some css tweaks in the editor to keep up with WP3.3
* added action hook "soma_column_data" to inject custom post type column data output

= 1.2 =
* added listings for public custom post types and taxonomies to the Right Now dashboard widget
* added ability to pick future years (+10) in the basic date picker

= 1.1.1 =
* bugfix: soma_metabox_data was expecting unecessary array keys
* bugfix: legacy date selectors couldn't handle mysqldate format
* bugfix: somaFunctions::fetch_featured_image() couldn't handle when wp uploads were organized in year-month folders. Also couldn't handle when all the sizes (thumb, medium, full) didn't exist... ugh...

= 1.1 =
* created public functions in api.php to initialize things like custom post type, taxonomy, terms, and custom metabox data
* added flush_rewrite_rules to plugin activation
* added contextual help customization per CPT
* generate custom icon paths automatically based on CPT slug, just provide URL to directory where they're located, image name scheme "slug-menu-icon.png"
* limit taxonomy term insertion to plugin or theme activation (two scenarios where soma_init_taxonomy could be called)

= 1.0 =
* first public release on wordpress.org

= 0.6 =
* added jPlayer for metaboxes - meta type Audio or Video
* asset_meta() can be set to serialize or not post_meta via somaMetaboxes::$meta_serialize var (default true), can also be overridden via function params
* somaMetaboxes::$meta_prefix var for themes to override
* added arg to init_taxonomy to automatically hide metaboxes on custom taxonomies

= 0.5 =
* added file upload field type
* added attachment gallery display field type
* added colorbox lightbox viewing for images, pdf, doc, xls, ppt (with google doc iframe viewer)
* added somaDownload class for creating links to download attachments directly
* added jqueryUI datepicker and timepicker

= 0.4 =
* added "help" metabox field type, displaying the text across both table columns
* fixed ridiculous metabox field table layout issues
* fixed saving of incomplete "date" fields
* included soma-admin-jquery.js
* NEW fetch_index function for dealing with $_GET and $_POST

= 0.3 =
* purged tons of outdated/unused code from other projects
* changed save_asset() for core data types to use wp_update_post instead of $wpdb->update
* NEW metabox field type: richtext (with tinymce)
* NEW functions for fetching userdata
* individual metabox save buttons

= 0.2 =
* First release
* added somaTypes class, handling generation of custom post types, taxonomies, and terms

= 0.1 =
* Code documentation is crude, with comments everywhere. Will standardize docs soon...
* includes somaFunctions, somaMetaboxes, somaSave, and somaSorter classes


== Upgrade Notice ==

= 1.7.4 =
Any metaboxes dealing with attachments should be revisited...

= 1.1.1 =
Nasty bugs squashed!

= 1.1 =
A bit more user-friendly with new public api calls...

= 1.0 =
Want to stay in sync? Install this version!

== Screenshots ==

1. Not much to say yet...
