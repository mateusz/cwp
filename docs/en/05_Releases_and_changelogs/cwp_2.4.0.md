# 2.4.0

## Overview

This upgrade includes CMS and Framework version 4.4.3.

 * [Framework 4.4.3](https://docs.silverstripe.org/en/4/changelogs/4.4.3/)

Upgrading to Recipe 2.4.0 is recommended for all sites. This upgrade can be carried out by any development team familiar with SilverStripe CMS. However, if you would like SilverStripe’s assistance, you can request support via the [Service Desk](https://www.cwp.govt.nz/service-desk/new-request/).

## New Features

The [release announcement](https://www.cwp.govt.nz/updates/news/cwp-2-4-has-landed) includes the note worthy features, but be sure to review the change log for full detail of all new features.

## Upgrading Instructions

In order to update an existing site to use the new basic recipe the following changes to your composer.json
can be made:

```json
"require": {
    "cwp/cwp-recipe-core": "2.4.0@stable",
    "cwp/cwp-recipe-cms": "2.4.0@stable",
    "silverstripe/recipe-blog": "1.4.0@stable",
    "silverstripe/recipe-form-building": "1.4.0@stable",
    "silverstripe/recipe-authoring-tools": "1.4.0@stable",
    "silverstripe/recipe-collaboration": "1.4.0@stable",
    "silverstripe/recipe-reporting-tools": "1.4.0@stable",
    "cwp/cwp-recipe-search": "2.4.0@stable",
    "silverstripe/recipe-services": "1.4.0@stable",
    "silverstripe/subsites": "2.3.2@stable",
    "tractorcow/silverstripe-fluent": "4.4.1@stable",
    "cwp/starter-theme": "3.0.1@stable"
},
"prefer-stable": true
```

### Major theme updates

The 3.0.x release lines of the Starter and Wātea themes, first available with CWP 2.3.0, are updated to use Bootstrap 4.x. Please [see the Bootstrap migration guide](https://getbootstrap.com/docs/4.3/migration/) for Bootstrap-specific changes. These updates also include an upgrade to Laravel Mix 4, along with other dependency upgrades (including Webpack 4 and Babel 7).

If you rely on either of these themes as a base for your own, the 3.x upgrade will be a fairly significant undertaking, so you may wish to keep using the latest 2.0.x release when upgrading to CWP 2.3.0 or later.

### Using MFA with Subsites

If you intend to adopt the new MFA module suite, you will need to ensure you are running Subsites 2.3.1 or later, as earlier versions are not compatible with MFA's authentication mechanisms. Composer will refuse to install MFA alongside an earlier version of Subsites.

## Security considerations

### HTTP Strict Transport Security Headers

The [HTTP Strict Transport Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security) (HSTS)
headers are an important security mechanism to reduce the chance of man-in-the-middle
attacks, by signaling to browsers that requests to the site should always
be encrypted (via accessing on the `https://` protocol).

CWP environments can always be accessed
via SSL, either through agency-provided certificates, or free certificates
provided through the Let's Encrypt service ([details](https://www.cwp.govt.nz/working-with-cwp/instance-management/ssl-certificates/)).
CWP websites already enforce the `https://` protocol for authenticated requests,
e.g. to `Security/*` and `admin/*`.

Until now, securing your site with HSTS has been a [secure coding](https://docs.silverstripe.org/en/4/developer_guides/security/secure_coding/)
recommendation in SilverStripe. New projects starting with CWP 2.4 will
automatically be configured to send HSTS headers, and redirect all requests to `https://`.

Existing projects can opt-in to this behaviour by copying
the new default configuration into their existing projects:
[app/_config/security.yml](https://github.com/silverstripe/cwp-installer/blob/master/app/_config/security.yml).

The default short-lived `max-age` for these headers is considered less secure,
and should be increased once you are confident that your website operates correctly
under SSL with HSTS for all domains. Please refer to [OWASP recommendations](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.md)
for secure `max-age` values (usually 365 days).

Note: This will only secure requests to SilverStripe.
In order to protect access to static assets,
consider adding HSTS headers to your `.htaccess` file,
and ensure that every environment (incl. local development)
are able to serve your site on the `https://` protocol.

There are other HTTP security headers that you should consider
to increase the security of your site. We recommend that you scan
your site on [securityheaders.com/](https://securityheaders.com/)
and implement additional headers depending on your use case
through `.htaccess` configuration.

Since SilverStripe is an extensible system, modules added
to your website or CMS might embed resources from other domains
which influence the settings on your particular website.
Common examples are videos embedded from youtube.com,
analytics loaded from google-analytics.com,
or captchas provided through spam protection modules
and loaded e.g. from google.com.

See [Working with Projects: Security](/working_with_projects/security) for more details.

<!--- Changes below this line will be automatically regenerated -->

## Change Log

### API Changes

 * 2019-08-02 [76adc1a](https://github.com/dnadesign/silverstripe-elemental/commit/76adc1a9fc897110c89a984771932328eceb8bb6) Deprecate ElementalSolrIndex (Ingo Schommer)
 * 2019-07-01 [282e83c](https://github.com/silverstripe/silverstripe-hybridsessions/commit/282e83c0ac1c48df2998305be66580dd41e0605e) McryptCrypto is now deprecated, use OpenSSLCrypto instead (Serge Latyntcev)

### Features and Enhancements

 * 2019-07-29 [1a4d04e](https://github.com/silverstripe/cwp/commit/1a4d04e8dc35b7fb74e70e9cff5db40854f2a9d6) NewsPage now has a getNewsPageAuthor() accessor for its conf… (#227) (Guy Marriott)
 * 2019-07-29 [beab891](https://github.com/silverstripe/cwp/commit/beab8919d6bc27e79e6064c062bb1ad874854d38) NewsPage now has a getNewsPageAuthor() accessor for its conflicted Author property (Robbie Averill)
 * 2019-07-26 [ef58f9c](https://github.com/silverstripe/cwp-installer/commit/ef58f9cc1b5bce6029eb7330d9fe8ae3a7584a3d) HTTP Strict Transport Security (Ingo Schommer)
 * 2019-07-26 [b1cf448](https://github.com/silverstripe/cwp-core/commit/b1cf44899dedf90fb7d7eacad33f0537388ba149) Opt-in HTTP Strict Transport Headers (Ingo Schommer)
 * 2019-07-26 [0391a79](https://github.com/tractorcow-farm/silverstripe-fluent/commit/0391a79c072ff309e79789fa4c6472fbcfab8b86) Configurable policies for handling the deletion of objects (#536) (Damian Mooyman)
 * 2019-07-25 [781e88c](https://github.com/dnadesign/silverstripe-elemental/commit/781e88ce8fe381dfa045073e5dc8acc5845160e5) Page level history now links directly into an elements history view (Robbie Averill)
 * 2019-07-17 [066be09](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/066be0934f1a41f9972b51b59ba49ec9644701ea) GridFieldQueuedExportButton is now Injectable (Robbie Averill)
 * 2019-07-14 [0b734c2](https://github.com/silverstripe/silverstripe-restfulserver/commit/0b734c21c68fae45fea9fd253e65b585d5766319) Aliases can now be defined for DataObject endpoints (#80) (Sander Hagenaars)
 * 2019-07-08 [30377cb](https://github.com/silverstripe/recipe-core/commit/30377cb03af85b0c00748dca1c9e8f215df4f4fa) | remove deprecated and unnecessary ErrorControlChainMiddleware from index.php (Serge Latyntcev)
 * 2019-06-28 [c25fa07](https://github.com/silverstripe/cwp-watea-theme/commit/c25fa078f310d1ebfe0731f5a5a779aa0e67ac43) Improve ARIA Landmarks by adjusting role attributes (Garion Herman)
 * 2019-06-28 [3cc4725](https://github.com/silverstripe/silverstripe-hybridsessions/commit/3cc4725328c3e46505e6b04b34b6764706a090f4) DatabaseStore binary safety methods exposed as API (Serge Latyntcev)
 * 2019-06-18 [4a8a4b7](https://github.com/silverstripe/cwp-core/commit/4a8a4b7c566922983331f2b285700d29130f1b65) Add PBKDF2 PasswordEncryptor with SHA-512 as the default algorithm for NZISM compliance (Robbie Averill)
 * 2019-05-16 [7a46b9b](https://github.com/bringyourownideas/silverstripe-maintenance/commit/7a46b9becb2c7d9bd6d257a7d39b34ccbee466c1) Update "More information" link to point to user help documentation instead of addons (Robbie Averill)
 * 2019-04-23 [07ea187](https://github.com/silverstripe/silverstripe-auditor/commit/07ea18793b920c0d8a740d27d86ba73f2cd82f69) Auditor now has hooks for silverstripe/mfa method login and registration actions (Robbie Averill)
 * 2019-04-05 [b5dd71b](https://github.com/dnadesign/silverstripe-elemental/commit/b5dd71b895395b0d74983bc4a68647e3eac87594) Content migration task has a bunch of new features...: (Guy Marriott)

### Bugfixes

 * 2019-08-26 [192dcae](https://github.com/silverstripe/cwp-core/commit/192dcaebdc07351fa5ce198ab9449e861171367d) Fix #74 textextraction config to enable it after 'textextractionconfig' defined in silverstripe/silverstripe-textextraction as well as using the use file caching as intended. (Charlie Bergthaler)
 * 2019-08-14 [f963ac4](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/f963ac46cd1e25eccba711087dd9bc9e3815675c) Fix the "clear link" action (#29) (Guy Marriott)
 * 2019-08-13 [8fdc227](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/8fdc227dc17dfe9e85982bbebf46212e0cfd594a) Add behat test for the block link field (Maxime Rainville)
 * 2019-08-13 [acbafb8](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/acbafb8970a61430b5568906157e4831d9a5304e) Update travis to run JS test and test PHP 7.3 (Maxime Rainville)
 * 2019-08-13 [d54288e](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/d54288ecc47f4958340671b1df3ceaa2fa35bc80) Add missing dev dependencies for the tests to run. (Maxime Rainville)
 * 2019-08-13 [d24bede](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/d24bede89c5938e7cb8bae42dbac0867be9ad1f2) Fix the the BlockLinkField clear action and update state on component update (Maxime Rainville)
 * 2019-07-31 [3864623](https://github.com/silverstripe/silverstripe-crontask/commit/3864623170d290c22a34bce39b2fd81073e2bf37) Fix the build to use xenial (Maxime Rainville)
 * 2019-07-26 [1ce8c3b](https://github.com/silverstripe/silverstripe-externallinks/commit/1ce8c3bbdf2fb5f7b3234198ef1bcee868a654b4) Add missing namespace import - unknown HTTP status codes are now handled (Robbie Averill)
 * 2019-07-24 [6e27953](https://github.com/silverstripe/cwp-watea-theme/commit/6e27953c141ff50d010f19c58427f5f1af7f71d3) Update selector for anchor tags to not target dropdown items (#102) (Guy Marriott)
 * 2019-07-24 [15c8144](https://github.com/silverstripe/cwp-watea-theme/commit/15c81444f907abb8637efae66aeb7452d3f77e34) Update selector for anchor tags to not target dropdown items (Sacha Judd)
 * 2019-07-24 [61d3d04](https://github.com/silverstripe/silverstripe-tagfield/commit/61d3d04ed60fc9b728de9d3091fdb534b0862f50) Removing potentially breaking lower-case change (and fix tests) (Guy Marriott)
 * 2019-07-24 [a1c57f6](https://github.com/silverstripe/silverstripe-tagfield/commit/a1c57f664db5828e26c3cef722b1c942611858cd) redux-form can now control tag fields (Guy Marriott)
 * 2019-07-23 [e2d7a6b](https://github.com/silverstripe/cwp-watea-theme/commit/e2d7a6b70c91209d80c13d86db70fcc0662c8723) Update dist files to pull in new typography styles from star… (#100) (Guy Marriott)
 * 2019-07-19 [d147111](https://github.com/tractorcow-farm/silverstripe-fluent/commit/d1471119a060d73e45370e824d2ea780fcd4674b) Fix import CheckboxSetField (Ian Patel)
 * 2019-07-18 [4df7fa2](https://github.com/dnadesign/silverstripe-elemental/commit/4df7fa235a55272d112b99c0473210208ad027b0) Element modifications are no longer persisted between page c… (#693) (Guy Marriott)
 * 2019-07-18 [e97a82f](https://github.com/silverstripe/silverstripe-tagfield/commit/e97a82f0b7d7484a16e783b9432847659f8b0a9d) Ensure tagfield is compatible with both React and Entwine contexts (Guy Marriott)
 * 2019-07-18 [2711b4f](https://github.com/silverstripe/cwp-watea-theme/commit/2711b4f65dabb19744ef9d5be11ab7f64539473e) Update dist files to pull in new typography styles from starter (Sacha Judd)
 * 2019-07-18 [c54f683](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/c54f683e953a87d9adf0bf889be0e86affe44676) Make remotepath optional to restore compatibility with CWP (Garion Herman)
 * 2019-07-17 [f734594](https://github.com/dnadesign/silverstripe-elemental/commit/f7345942ad4f2c2c1f454e32960afe73b66f7862) Drop the TinyMCE toolbar but increase the row count (Guy Marriott)
 * 2019-07-17 [124055f](https://github.com/silverstripe/cwp-watea-theme/commit/124055f4a2c437321ed571fb914e8328b0229124) Add missing aria-current to nav (#98) (Guy Marriott)
 * 2019-07-17 [1eae700](https://github.com/silverstripe/cwp-watea-theme/commit/1eae70029e0740a2a6ade7fe676ab415b648622f) Add missing aria-current to nav (Sacha Judd)
 * 2019-07-17 [806c2c1](https://github.com/dnadesign/silverstripe-elemental/commit/806c2c15cc7180abe45e4bfa032a6c0885d0f47b) LiteralField and LabelField now have correct padding when us… (#694) (Guy Marriott)
 * 2019-07-17 [967bae4](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/967bae4c87ee6d6f2c3d9219a41938173c2e5e5b) SitewideContentReport can now be extended to allow support for GridFieldQueuedExport on large projects (Robbie Averill)
 * 2019-07-17 [3a8c311](https://github.com/dnadesign/silverstripe-elemental/commit/3a8c311fbdb560d0977a3210f474f9879dc2049d) LiteralField and LabelField now have correct padding when used in inline edit forms (Robbie Averill)
 * 2019-07-17 [1246691](https://github.com/dnadesign/silverstripe-elemental/commit/1246691605c3d41c7e59ac5404497afffd4f7d2d) Element modifications are no longer persisted between page changes with PJAX (Robbie Averill)
 * 2019-07-16 [0b3beef](https://github.com/dnadesign/silverstripe-elemental/commit/0b3beeff1b35ceac47ee1dbc21b6651683f3481a) Non-inline editable element edit links are now absolute, fix… (#690) (Guy Marriott)
 * 2019-07-16 [4b13a9f](https://github.com/dnadesign/silverstripe-elemental/commit/4b13a9f02eed2920784f96abd12d62d074b639e1) Element validation can now be used, and elements with valida… (#691) (Guy Marriott)
 * 2019-07-15 [f920b7e](https://github.com/dnadesign/silverstripe-elemental/commit/f920b7e3955192ced4bfb4bccd9687d40c805a3e) Call onBeforeWrite() to ensure a sort order is assigned in lieu of a full write (Robbie Averill)
 * 2019-07-15 [fbfead9](https://github.com/silverstripe/silverstripe-comments/commit/fbfead9c9ed83581780c7cfb0cd5c2e4b780e100) CommentAdmin implements PermissionProvider (Jason Irish)
 * 2019-07-15 [707cd95](https://github.com/dnadesign/silverstripe-elemental/commit/707cd95b01bf88cf1ca22aa49c144d9445b076eb) Error "cannot convert undefined or null to object" when no inline editable forms are loaded yet (Robbie Averill)
 * 2019-07-15 [f7ccc45](https://github.com/dnadesign/silverstripe-elemental/commit/f7ccc4509302374cf3adaf466f70ff632ba2f4ea) Element validation can now be used, and elements with validation rules can be added (Robbie Averill)
 * 2019-07-15 [9c6c469](https://github.com/dnadesign/silverstripe-elemental/commit/9c6c469dfe5d4e9eca3ecab8ef7ae86e21501af4) Non-inline editable element edit links are now absolute, fixes IE11 issue (Robbie Averill)
 * 2019-07-15 [f0c8715](https://github.com/silverstripe/cwp-watea-theme/commit/f0c8715ccd2329d56427a8426cacc23bbe830a93) Remove btn-link styling and add colour picker to btn-secondary (Sacha Judd)
 * 2019-07-14 [f90cb17](https://github.com/silverstripe/recipe-core/commit/f90cb17c552356cfe34467c37194e73165aee18f) Travis PHP versions (#46) (Guy Marriott)
 * 2019-07-12 [9e53544](https://github.com/silverstripe/cwp-watea-theme/commit/9e535447c86149807a9e1849ae5267acd41694c5) Revert btn btn-link for fix in starter (#94) (Guy Marriott)
 * 2019-07-10 [c6b3e34](https://github.com/silverstripe/silverstripe-crontask/commit/c6b3e3455ae984a7880e60f1e8c71420db6635ea) Treat empty schedule value as task-disabled. (Sam Minnee)
 * 2019-07-10 [c34f720](https://github.com/silverstripe/cwp-watea-theme/commit/c34f720bd0142b8cc40cc8b3cd10081a3b9196e9) Ensure consistency for search across the colour picker themes (Sacha Judd)
 * 2019-07-09 [30bec12](https://github.com/silverstripe/cwp-watea-theme/commit/30bec1240525bb14ed76e268c54d300b52576a59) Add accessible name to reflect components function and  active styling (Sacha Judd)
 * 2019-07-09 [44aed9c](https://github.com/silverstripe/silverstripe-realme/commit/44aed9cc9b578e3b38dcbc721679357b5322432d) Fix overseas RealMe contact phone (Indy Griffiths)
 * 2019-07-08 [1819336](https://github.com/silverstripe/cwp-agencyextensions/commit/181933682a15d6db3e760d81e79cd84e9df4d935) Add Carousel title field for screen readers (Sacha Judd)
 * 2019-07-08 [cf8f0b3](https://github.com/silverstripe/recipe-core/commit/cf8f0b3961e62aaa52ab8f29ab452a29966cc37a) Travis PHP versions (Serge Latyntcev)
 * 2019-07-08 [6acb2f4](https://github.com/silverstripe/cwp-watea-theme/commit/6acb2f44ec984eac249732db522489f920c45792) Revert btn btn-link for fix in starter (Sacha Judd)
 * 2019-07-08 [ed11267](https://github.com/silverstripe/cwp-watea-theme/commit/ed11267ac343f70f65faf57b4f2adb46194c8a23) Remove gray-400 from nav links and add to hover instead (#89) (Guy Marriott)
 * 2019-07-08 [e3a8b21](https://github.com/silverstripe/cwp-watea-theme/commit/e3a8b21342b815aaafb717c255bfc7f75f425efc) Add colour picker to carousel indicators for accessibility re… (#92) (Guy Marriott)
 * 2019-07-07 [70d2790](https://github.com/silverstripe/cwp-watea-theme/commit/70d279050cea616e6ca0c07e90501af48df44e56) Add text-decoration underline to quicklinks and showcases (#90) (Guy Marriott)
 * 2019-07-07 [e991612](https://github.com/silverstripe/cwp-watea-theme/commit/e991612eb608181a1f72995cf6c7f82624a879d6) Add carousel accessibility requirements for WCAG 2.0 (Sacha Judd)
 * 2019-07-07 [03a3b3a](https://github.com/silverstripe/cwp-watea-theme/commit/03a3b3adfaaa40c9c39a23a8244eb4223591f0ca) Remove btn btn link to remove default bootstrap styling from… (#93) (Guy Marriott)
 * 2019-07-04 [eeeee9e](https://github.com/silverstripe/cwp-watea-theme/commit/eeeee9e338d27cdda7381bf8de353653c5674712) Add colour picker to carousel indicators for accessibility requirements (Sacha Judd)
 * 2019-07-04 [1f5df6f](https://github.com/silverstripe/cwp-watea-theme/commit/1f5df6f79f81990cd7bfb5ec7dc7630e5d3f1d35) Remove btn btn link to remove default bootstrap styling from navbar-caret (Sacha Judd)
 * 2019-07-04 [d686ea2](https://github.com/silverstripe/cwp-watea-theme/commit/d686ea29986afe9f6cae876d1217272050fdabbb) Add text-decoration underline to quicklinks and showcases (Sacha Judd)
 * 2019-07-04 [8d86ff8](https://github.com/silverstripe/cwp-watea-theme/commit/8d86ff873ae11daffc5bb9475116cacafd35ba17) Remove gray-400 from nav links and add to hover instead (Sacha Judd)
 * 2019-07-01 [7005957](https://github.com/silverstripe/silverstripe-hybridsessions/commit/70059579c5b3bdb5d532ac611cc0613fac1ccadc) Add phpcs ruleset and reformat for PSR-12 (Robbie Averill)
 * 2019-06-30 [99b4f7c](https://github.com/silverstripe/silverstripe-hybridsessions/commit/99b4f7c16886803c0af5e0b5862d85ad6dac95f7) DatabaseStore binary safety (Serge Latyntcev)
 * 2019-06-28 [54db49a](https://github.com/silverstripe/cwp-watea-theme/commit/54db49aa0e382f67b659ebdcbd307d9af1096ea2) Content block titles no longer have an inconsistent font size (Robbie Averill)
 * 2019-06-28 [86c311f](https://github.com/silverstripe/cwp-watea-theme/commit/86c311f77fdeaf96833cda30a7ce8eb0404f41dc) Footer copyright text is now visible against dark backgrounds (Robbie Averill)
 * 2019-06-28 [3fc96cd](https://github.com/silverstripe/cwp-core/commit/3fc96cd2b3a3d3a612a2297b372e47d696ffa5b1) "external link" screen reader label is now translatable (Robbie Averill)
 * 2019-06-28 [981cb28](https://github.com/silverstripe/cwp-watea-theme/commit/981cb28af4c0a178959178425f50fc0de5f9f994) Add tabindex to focus the results notification message (Sacha Judd)
 * 2019-06-27 [c582cc5](https://github.com/silverstripe/cwp-watea-theme/commit/c582cc5cfd12318a3340cba50dd516cdec6b40e0) Add aria-labels and remove redundant span and title attributes (Sacha Judd)
 * 2019-06-27 [72914df](https://github.com/silverstripe/cwp-watea-theme/commit/72914dff731ea03919154cc09715d92f8fe13ecd) Add aria-current attribute to selected page nav links (Sacha Judd)
 * 2019-06-27 [b8e5da6](https://github.com/silverstripe/cwp-watea-theme/commit/b8e5da67c7a128a2141b6fabf99672fb6db106f7) Add aria-label to Language selector for narrow viewports (Sacha Judd)
 * 2019-06-26 [242e5a3](https://github.com/silverstripe/silverstripe-textextraction/commit/242e5a307d0b1f6beb3cea31abba370ca50042e4) Change check for cleanup of temp files only if file is instance of File. (Charlie Bergthaler)
 * 2019-06-23 [4fdf2e2](https://github.com/silverstripe/silverstripe-subsites/commit/4fdf2e24e328c714b571d47b5dfb5b64fc5c185b) LeftAndMainSubsites::canAccess() now accepts a Member argument and falls back to the session member (Robbie Averill)
 * 2019-06-20 [a9270d7](https://github.com/silverstripe/silverstripe-textextraction/commit/a9270d73adfd2d0bf35447a478505dee6e759ff0) Cleanup temporary file after extracting content in TikaServerTextExtractor and TikaTextExtractor (Charlie Bergthaler)
 * 2019-06-18 [a5cd23c](https://github.com/silverstripe/cwp-core/commit/a5cd23c97a93b8509271dc64987111a77c5b703b) Fix unit test errors when hash_pbkdf2 is not passed a string for password (Robbie Averill)
 * 2019-06-14 [b1935a5](https://github.com/dnadesign/silverstripe-elemental/commit/b1935a5e045195bf49bf4ae47e2305bcf53070aa) Upgrade vulnerable dependencies (Garion Herman)
 * 2019-06-13 [70c630e](https://github.com/dnadesign/silverstripe-elemental/commit/70c630e578b1e311b51b442ef6ee2ea86f7aa0f7) Upgrade jQuery to patch vulnerability (Garion Herman)
 * 2019-05-30 [1f51fcd](https://github.com/silverstripe/silverstripe-subsites/commit/1f51fcd90944ea1587c5c98acf00c71b70e47795) Subsites virtual pages now allow you to re-save them when used in conjunction with silverstripe-fluent (Robbie Averill)
 * 2019-05-30 [c60acb3](https://github.com/silverstripe/silverstripe-subsites/commit/c60acb31906af5efc8182ff55c98b82f59a184d9) Field labels for subsites virtual pages are no longer repeated (Robbie Averill)
 * 2019-05-30 [4d7641e](https://github.com/silverstripe/silverstripe-subsites/commit/4d7641e16a50e1c4184710f79a08e70af426f0e5) allowed pagetypes displaying incorrectly when switching subsite (Garion Herman)
 * 2019-05-30 [83f9fb9](https://github.com/tractorcow-farm/silverstripe-fluent/commit/83f9fb975e3de9394f49703b3cc063829406ceb2) Fluent now respects existing base URL prefixes in URL segment fields when no fluent domain exists (Robbie Averill)
 * 2019-05-30 [1e44e1d](https://github.com/silverstripe/silverstripe-subsites/commit/1e44e1d4bad737f310af7e51a95ac0c91f69072c) Domains now default to "Automatic" protocol, and have the correct help description (Robbie Averill)
 * 2019-05-30 [59ecca8](https://github.com/symbiote/silverstripe-advancedworkflow/commit/59ecca89d879414846ac9fb5b91b5fc91110cfcb) Call FieldList::isReadonly() if it exists otherwise default to existing behaviour (Robbie Averill)
 * 2019-05-27 [d7c76ec](https://github.com/silverstripe/silverstripe-userforms/commit/d7c76ecf80ef4791403b028b07ab65dba21be79c) Preview email link now handles cases where it's loaded in the browser, requested via AJAX and used in a trait or a page context (#887) (Guy Marriott)
 * 2019-05-20 [f4cd7a3](https://github.com/silverstripe/silverstripe-userforms/commit/f4cd7a3836dc1ec2c462dc0778d1b155ad21faa6) Allowed text length fields now align correctly with each other (#886) (Guy Marriott)
 * 2019-05-17 [9aae076](https://github.com/dnadesign/silverstripe-elemental/commit/9aae0766aa5eec480c5f008845f5d3811ff299ec) ElementalCMSMainExtension is now enabled, fixes double search class filter 'All pages' (Robbie Averill)
 * 2019-05-17 [483fbc8](https://github.com/silverstripe/silverstripe-userforms/commit/483fbc8499a5735a79cbe42a47419b90b682c129) Preview email link now handles cases where it's loaded in the browser, requested via AJAX and used in a trait or a page context (Robbie Averill)
 * 2019-05-17 [d0e937a](https://github.com/silverstripe/silverstripe-userforms/commit/d0e937a5883e5bf4aecea8442d746264717df76a) Allowed text length fields now align correctly with each other (Robbie Averill)
 * 2019-05-17 [5c16689](https://github.com/dnadesign/silverstripe-elemental/commit/5c166892acb07930fc7f1d255b973d3c64623d3f) Don't leave pages in draft when adding ElementalAreasExtension (#669) (Guy Marriott)
 * 2019-05-17 [5cba1e8](https://github.com/symbiote/silverstripe-advancedworkflow/commit/5cba1e8e13a11733db26cabae38a803ea69c9b96) Paragraphs inherit the diff (added/deleted) background colour in workflow transition UI (#398) (Guy Marriott)
 * 2019-05-16 [a1b3fa7](https://github.com/dnadesign/silverstripe-elemental/commit/a1b3fa78496d9daa0b2c55d3932bd5421da8e05f) Don't leave pages in draft when adding ElementalAreasExtension (Guy Marriott)
 * 2019-05-16 [9082db1](https://github.com/silverstripe/silverstripe-iframe/commit/9082db159c62432716a82675053eeb637501f440) Add CMS configurable title for iframe to tell screenreaders it contains frame content (Robbie Averill)
 * 2019-05-16 [181e0de](https://github.com/silverstripe/silverstripe-userforms/commit/181e0de171f92b01401b1e36319e322e64900941) Multi page userforms now display their step titles, which were previously broken (Robbie Averill)
 * 2019-05-16 [e179887](https://github.com/symbiote/silverstripe-advancedworkflow/commit/e179887e9b53f979c2c99e82bcc97f0e3926ac50) Paragraphs inherit the diff (added/deleted) background colour in workflow transition UI (Robbie Averill)
 * 2019-05-14 [5c60f4b](https://github.com/silverstripe/silverstripe-ldap/commit/5c60f4baceb203f498daf41311da5f6a011c8edd) prevents users being removed from the LDAPService::$default_group (Tim Kung)
 * 2019-05-10 [83c3688](https://github.com/silverstripe/cwp-watea-theme/commit/83c3688bbab5d231d01e18298d2d419096f772b0) List items now have the same font weight as paragraphs (Robbie Averill)
 * 2019-05-09 [e313f2e](https://github.com/silverstripe/silverstripe-subsites/commit/e313f2ed5d713bc1ca90223e892c39ce43ac85ee) Update Behat assertion to use correct label for "Search or choose Page" (Robbie Averill)
 * 2019-05-09 [536420e](https://github.com/silverstripe/silverstripe-subsites/commit/536420ec687db26dcd355fd3cf969aeed6d61106) Update Behat assertion to use correct field label for SilverStripe 4.4 (Robbie Averill)
 * 2019-05-09 [f65f5b5](https://github.com/silverstripe/silverstripe-comments/commit/f65f5b569777b51db1a3c04555b6472b4f1c0bc2) Remove reliance on translations in fieldLabels test, run textcollector, remove deprecated code from CommentsTest (Robbie Averill)
 * 2019-05-07 [4984023](https://github.com/silverstripe/silverstripe-restfulserver/commit/498402389c47b6a148c6b284c9b2917caee24f5c) Fixes #70 Added extension points for GET requests (User for performing fabric deployments)
 * 2019-05-03 [56ab977](https://github.com/silverstripe/cwp-search/commit/56ab977944ffea8384408abc860e06a098639b1a) Automatically redirect index action to SearchForm action (#22) (Guy Marriott)
 * 2019-05-02 [80c32bd](https://github.com/silverstripe/cwp-search/commit/80c32bd23460b501bc9700d68d6667ccfff5602e) Automatically redirect index action to SearchForm action (Robbie Averill)
 * 2019-04-29 [3f19c0a](https://github.com/dnadesign/silverstripe-elemental/commit/3f19c0ac05216b162e22a7f11571833735b96ec1) Ensuring write operations when clearing content is captured in a try...catch (Guy Marriott)
 * 2019-04-25 [257d0d5](https://github.com/dnadesign/silverstripe-elemental/commit/257d0d54c28637a564047df7b1210dde9aa9905d) updateAvailableTypesForClass() extension $class param (Christopher Darling)
 * 2019-04-17 [ead0fba](https://github.com/silverstripe/silverstripe-tagfield/commit/ead0fbac6b23e469e9c6e4a5708e45ca58119f06) fixed the issue with filters being taken off from rendering values (Nivanka Fonseka)
 * 2019-04-06 [7eae780](https://github.com/dnadesign/silverstripe-elemental/commit/7eae780835e8191cbaab868bbc1f3f1ce45343d4) Only publish items that were previously published & adding docs (Guy Marriott)
 * 2019-03-27 [4b0eacf](https://github.com/tractorcow-farm/silverstripe-fluent/commit/4b0eacf9cd13b60d4c00f89ac88f60c25624ffc1) fix index when fluent is in use and there is no fallback locale (Aljoša Balažic)
 * 2018-06-26 [01c1ead](https://github.com/silverstripe/silverstripe-blog/commit/01c1ead069825c383fd31e72b35d835da65be558) Fix blog archive widget bug (3Dgoo)

### Other changes

 * 2019-09-11 [eb8b358](https://github.com/silverstripe/cwp/commit/eb8b35864dbc500760f98cf9e675cea274b95aad) DOC Add EOL dates for CWP 2.3.x (Garion Herman)
 * 2019-09-08 [081f0ff](https://github.com/silverstripe/cwp-core/commit/081f0ff94e5ae25e030573426956f543eb8bf605) Increase iterations used by PBKDF2 per security recommendation (Garion Herman)
 * 2019-09-05 [d7634ab](https://github.com/silverstripe/cwp/commit/d7634abf65cc83768a6652bf74c10ae703201fa1) DOCS HSTS clarification on max-age (Ingo Schommer)
 * 2019-08-20 [0cdf588](https://github.com/silverstripe/cwp/commit/0cdf588dd487a66edb51ad32e9775489e157e469) Update Travis config to use Xenial (#231) (Guy Marriott)
 * 2019-08-20 [ed9cc1a](https://github.com/silverstripe/cwp/commit/ed9cc1a152236e84581cc619e8f6682d8dfdd7c1) Update Travis config to use Xenial (Garion Herman)
 * 2019-08-20 [839cbb7](https://github.com/silverstripe/silverstripe-externallinks/commit/839cbb7185f9ac48c9245848fcef436a60c7a13c) Update translations (Guy Marriott)
 * 2019-08-20 [c177845](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/c1778452bd409e334602dc95ca3284dc21cf8b6d) Update translations (Guy Marriott)
 * 2019-08-20 [8beb948](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/8beb948e5650a0bc6d8d0b13c990975ed79936bd) Update translations (Guy Marriott)
 * 2019-08-20 [a3f28bb](https://github.com/silverstripe/silverstripe-iframe/commit/a3f28bb58b981cda3ba3a5335b99b25b0d1eb1c2) Update translations (Guy Marriott)
 * 2019-08-20 [ac45c4c](https://github.com/silverstripe/cwp-core/commit/ac45c4ccf1f093821dc767a82feca30f67c9648d) Update translations (Guy Marriott)
 * 2019-08-20 [d06fe86](https://github.com/silverstripe/silverstripe-blog/commit/d06fe86d54b474f3dc7abf74354c4cf99729608c) Update translations (Guy Marriott)
 * 2019-08-20 [1d2f0ac](https://github.com/silverstripe/cwp/commit/1d2f0acce289619f90f4571df98557927d0882b3) Update translations (Guy Marriott)
 * 2019-08-20 [e21a092](https://github.com/silverstripe/silverstripe-comments/commit/e21a09234a3070d3c869218739c9d45f168ced41) Update translations (Guy Marriott)
 * 2019-08-19 [9148a58](https://github.com/silverstripe/recipe-cms/commit/9148a589a8a78db1b9561fa4b17187e552b234b0) Update development dependencies (Guy Marriott)
 * 2019-08-19 [6b71113](https://github.com/silverstripe/recipe-core/commit/6b71113aff25b536fdfe1c31a55a9121f741209d) Update development dependencies (Guy Marriott)
 * 2019-08-16 [9425139](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/94251390d612ec5d6c895b81dd24176e765cb792) Increase memory limit for kitchen sink builds (Robbie Averill)
 * 2019-08-15 [d2a295d](https://github.com/symbiote/silverstripe-advancedworkflow/commit/d2a295d28e12a60743980b197fb19227f8980c10) Use trusty distro in Travis builds and update tested SilverStripe versions (Robbie Averill)
 * 2019-08-15 [8f1549c](https://github.com/silverstripe/recipe-content-blocks/commit/8f1549c73bfb1d710b9bc80bc0f66dfe6a9825ba) Bump silverstripe-elemental to 4.2.x (Robbie Averill)
 * 2019-08-15 [c7ed94a](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/c7ed94abb751d7be98a00d0171d40b229c14d9fd) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [8afcb28](https://github.com/silverstripe/recipe-reporting-tools/commit/8afcb28d1967e7feb32eb6a58e2497c67ba6d96b) Use trusty distro in Travis builds and add PHP 7.3 to Travis (Robbie Averill)
 * 2019-08-15 [03d31b2](https://github.com/silverstripe/recipe-form-building/commit/03d31b2844e1e0cb7704ba532642578e38530b1a) Use trusty distro in Travis builds and add PHP 7.3 to Travis (Robbie Averill)
 * 2019-08-15 [8da5008](https://github.com/silverstripe/recipe-content-blocks/commit/8da500845ab5e1f6d63b683d6d59ebbe2a557285) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [08aeba9](https://github.com/silverstripe/recipe-collaboration/commit/08aeba9819f26beb5345fbaeb9498aa895aafb22) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [1a9e9e3](https://github.com/silverstripe/recipe-authoring-tools/commit/1a9e9e3a89a7105c48340a17dde301266c8d7ea7) Add PHP 7.3 to Travis (Robbie Averill)
 * 2019-08-15 [98f7f0b](https://github.com/silverstripe/recipe-authoring-tools/commit/98f7f0b85a67388fa852099f6d0aecd5c71405e8) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [338fe15](https://github.com/bringyourownideas/silverstripe-maintenance/commit/338fe157fe1eddf8a7ef8a615b28d09b6eba238c) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [7d17c8e](https://github.com/silverstripe/silverstripe-iframe/commit/7d17c8eea3dbc9cc8c4dc4cc9730b3dc5221e57f) Use trusty distro in Travis builds and update tested SilverStripe versions (Robbie Averill)
 * 2019-08-15 [121aefb](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/121aefbdf3c497b043f093c93e27e383892dd5a1) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [2b612e9](https://github.com/silverstripe/cwp-recipe-core/commit/2b612e9ec0a13fd8dffa0c860c0085328111e4d5) Add PHP 7.3 to Travis and reduce versioned in Travis to 1.4.x (Robbie Averill)
 * 2019-08-15 [d3da3da](https://github.com/silverstripe/cwp-recipe-core/commit/d3da3dae60f62dae5643cf2f5db5bd50c78d104c) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [4b09cb2](https://github.com/silverstripe/cwp-core/commit/4b09cb2bf5061292854f65d9bcbf5cda3320edf5) Reduce SilverStripe to 4.4.x in Travis builds (Robbie Averill)
 * 2019-08-15 [f909053](https://github.com/silverstripe/cwp-core/commit/f909053f761360ac74ae44410b7159705d8d487f) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [40eb69e](https://github.com/silverstripe/silverstripe-blog/commit/40eb69ef6238e827bf23a1fa38ae32b553d89081) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-08-15 [378d6de](https://github.com/silverstripe/silverstripe-auditor/commit/378d6de3d37dfc4842ca57def050481dd28ecfa8) Update Travis to use trusty and existing SilverStripe versions (Robbie Averill)
 * 2019-08-14 [10e0898](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/10e0898fd2bcda94e7aeb5530efef76f623fda7a) Update agency-extensions and gridfieldqueuedexport (Robbie Averill)
 * 2019-08-14 [50c1693](https://github.com/silverstripe/cwp-installer/commit/50c169355c3a891c80ebc6d6e0409a049a56c6ed) Update fluent to 4.4.x (Robbie Averill)
 * 2019-08-14 [4b165d6](https://github.com/silverstripe/recipe-authoring-tools/commit/4b165d63b862d8b938a09d1b1a479e55229c13c4) Update restfulserver (Robbie Averill)
 * 2019-08-14 [3333214](https://github.com/silverstripe/recipe-reporting-tools/commit/3333214f9cbbb11ae29f2e3baf604fea794c9ce9) Update silverstripe-maintenance to 2.3.x (Robbie Averill)
 * 2019-08-14 [acfb8db](https://github.com/silverstripe/recipe-authoring-tools/commit/acfb8db66c2c4fe719304908d7fc52569282a055) Update tagfield to 2.4.x (Robbie Averill)
 * 2019-08-14 [288ea4b](https://github.com/silverstripe/recipe-blog/commit/288ea4ba10d5890ef3e8014ef2b0be6b96202618) Update blog to 3.4 (Robbie Averill)
 * 2019-08-14 [eff7e19](https://github.com/silverstripe/cwp-recipe-core/commit/eff7e19d95078bfd73711daa30160731eb968e61) Update auditor and hybridsessions (Robbie Averill)
 * 2019-08-14 [d615873](https://github.com/silverstripe/recipe-reporting-tools/commit/d615873cff34349391a066e9a629a4eb12040239) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [d3d7f57](https://github.com/silverstripe/recipe-content-blocks/commit/d3d7f5737f46427289b0e4be7c0bc9ea5b081f0a) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [91e7edf](https://github.com/silverstripe/recipe-blog/commit/91e7edf79924bca0b1ee32cb5dc069cffe272ba9) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [5cd4170](https://github.com/silverstripe/recipe-authoring-tools/commit/5cd4170194a9684ff686c47298f4ad4bcabca0ce) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [f8c3c3b](https://github.com/silverstripe/recipe-form-building/commit/f8c3c3bc474a3a909ba5262bbc6aed785d9e62a7) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [899dfe4](https://github.com/silverstripe/recipe-collaboration/commit/899dfe48c3a73b1d621f2a9466f4b0d4df73b4ba) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [4f6bcfa](https://github.com/silverstripe/recipe-authoring-tools/commit/4f6bcfab83df31b4d8724c0deb5f21d1efa8179e) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [28c4142](https://github.com/silverstripe/cwp-recipe-cms/commit/28c41429cc22cfb7b61104d3213ee6efbc3cb2bb) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [c5451b5](https://github.com/silverstripe/cwp-recipe-core/commit/c5451b5825e53749d5cb7cb09a6b54ef6745da67) Switch to SilverStripe 4.4.x (Robbie Averill)
 * 2019-08-14 [b8ff2b3](https://github.com/silverstripe/cwp-core/commit/b8ff2b3e1d89fa108026c31e33fcb6001acae2f1) Switch core version to 4.4.x and increase PHP to 7.1 (Robbie Averill)
 * 2019-08-13 [e8f7bfc](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/e8f7bfca5022d8a52f03786f94baf7122bf09db7) Implement peer review feedback (Maxime Rainville)
 * 2019-08-13 [b88f3c7](https://github.com/silverstripe/cwp-recipe-core/commit/b88f3c7f5d380f920bc5892af855ff46113187cd) Bump environmentcheck to match 2.3.2 release dependency line (Robbie Averill)
 * 2019-08-13 [2f70fd3](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/2f70fd3a6e71f4a85e2c115ec286b8907ea83545) Add missing MainContextAwareTrait to FeatureContext (Maxime Rainville)
 * 2019-08-13 [34b5a43](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/34b5a43f4b4fd23314aca3e6cb067c789ccb24d7) Ignore everything under vendor when linting (Maxime Rainville)
 * 2019-08-13 [87c9b26](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/87c9b262b89ffac80a503c68719efeb80074bb8e) Ignore vendor everything under vendor (Maxime Rainville)
 * 2019-08-13 [242eb03](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/242eb03ea39bd44c3d134a3911cfa77819f6368e) Build admin before trying to run our tests (Maxime Rainville)
 * 2019-08-13 [b2f2d46](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/b2f2d46018dc0550842583b7061faa35771ed083) Add .nvmrc file to target node 6 on travis builds (Maxime Rainville)
 * 2019-08-13 [163d942](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/163d94284093303dbf78faecc3be28377139a916) Rebuild library (Maxime Rainville)
 * 2019-08-04 [4c6776e](https://github.com/dnadesign/silverstripe-elemental/commit/4c6776e92299a237bb26c7584f4195d9c4febfa0) Bump lodash from 4.17.11 to 4.17.15 (dependabot[bot])
 * 2019-08-04 [86785c3](https://github.com/dnadesign/silverstripe-elemental/commit/86785c3386a9ae70fc262c081007620459b70827) Reduce line length (Robbie Averill)
 * 2019-07-31 [6bd547e](https://github.com/silverstripe/silverstripe-crontask/commit/6bd547e0957bcd0fabea96308bed6ed5380dda5d) DOC Explain the falsy behaviour of getSchedule() on the CronTask interface. (Maxime Rainville)
 * 2019-07-30 [f16ce3f](https://github.com/dnadesign/silverstripe-elemental/commit/f16ce3f9dd7b5bbe10df0cd676b0e67428d15cbf) Remove temporary state from BaseElement and rely on CMSEditLink parameter instead (Guy Marriott)
 * 2019-07-30 [68b1b19](https://github.com/tractorcow-farm/silverstripe-fluent/commit/68b1b191698e23f32e7dd972fb06b9da39321e6e) Revert "FIX Fluent now respects existing base URL prefixes in UR… (#539) (Guy Marriott)
 * 2019-07-30 [3a37dca](https://github.com/tractorcow-farm/silverstripe-fluent/commit/3a37dcae6da7c717dd50f7b64ffe230679e9a801) Revert "FIX Fluent now respects existing base URL prefixes in URL segment fields when no fluent domain exists" (Damian Mooyman)
 * 2019-07-29 [a9d63b1](https://github.com/dnadesign/silverstripe-elemental/commit/a9d63b1d3b5c0fda9c2305396966e77f52791a20) DOCS Syntax fixes and links (Ingo Schommer)
 * 2019-07-29 [49adcd0](https://github.com/tractorcow-farm/silverstripe-fluent/commit/49adcd0e04623351bb0f1df0961c64fa22ff4f77) Remove changelog - see GitHub releases for release notes (Robbie Averill)
 * 2019-07-29 [bb56d33](https://github.com/silverstripe/cwp/commit/bb56d334325d7cb0c454b31f29a8e96b4d291b6d) DOCS Include 2.3.2 in the index page of the releases doc (Guy Marriott)
 * 2019-07-29 [0f121d6](https://github.com/silverstripe/cwp/commit/0f121d69454c64225e5d911595327f6b62b9fa3b) DOCS Add mention of Solr reconfigure issue in "known issues" section of 2.3.0 (Guy Marriott)
 * 2019-07-29 [1d899f5](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/1d899f5e49d578571cabfe001e5271b17984a3cd) DOCS Correct typo in changelog template (and remove "CMS") (Guy Marriott)
 * 2019-07-26 [b39a81b](https://github.com/silverstripe/silverstripe-externallinks/commit/b39a81b60b63c592793ca85e24ef0662cd80e5f6) Use trusty in Travis builds (Robbie Averill)
 * 2019-07-26 [7a33572](https://github.com/silverstripe/silverstripe-externallinks/commit/7a335726c481613e74f62206370699a56dcec709) Remove SilverStripe 4.0-4.2 from Travis builds (Robbie Averill)
 * 2019-07-26 [18eb0fa](https://github.com/silverstripe/cwp/commit/18eb0fa0f9fdcf49b04d1691690f65602f7e5f8b) DOCS HTTP Strict Transport Security (Ingo Schommer)
 * 2019-07-25 [afc4f57](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/afc4f571486a5f81148a809d832568bd01755d21) Enable color and font pickers by default (#42) (Guy Marriott)
 * 2019-07-25 [07db319](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/07db319b88110b83bb96f960a30be8432ad76e26) Enable color and font pickers by default (Ingo Schommer)
 * 2019-07-25 [bd84139](https://github.com/silverstripe/silverstripe-tagfield/commit/bd84139b968ecd1e143647aa2df4e2e4066cd3d1) Code clean-up (Guy Marriott)
 * 2019-07-24 [804c6ba](https://github.com/silverstripe/silverstripe-tagfield/commit/804c6bac2fec2782b6928a8598577d7da9d9fba0) Run automated phpcs linting (Robbie Averill)
 * 2019-07-22 [b8c0a07](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/b8c0a07252dbde21734b2d32ebc519835102e96f) Add inline requirements for MFA modules in Travis builds for PHP 7.1 (Robbie Averill)
 * 2019-07-22 [6b28dd9](https://github.com/dnadesign/silverstripe-elemental/commit/6b28dd925658780e0739f8169b3ab41dbf25590c) Reintroduce statement for $editorField resolving correctly (Robbie Averill)
 * 2019-07-21 [d23f3fc](https://github.com/dnadesign/silverstripe-elemental/commit/d23f3fc04c1cc2c0ecd5f6867fc9d69f3fcd1d45) Shift TinyMCE field adjustments back to EditFormFactory (Garion Herman)
 * 2019-07-19 [e2b89bc](https://github.com/silverstripe/cwp-agencyextensions/commit/e2b89bce57cc9519835b428acdf98c76578468fc) Use specific recipe versions in Travis builds (Robbie Averill)
 * 2019-07-19 [9f77ec4](https://github.com/silverstripe/cwp-agencyextensions/commit/9f77ec47ee2f356ee36f5364bcd96fd081d38517) Change recipe-cms 1.x to 4.x (Robbie Averill)
 * 2019-07-19 [bc2b3a9](https://github.com/silverstripe/silverstripe-realme/commit/bc2b3a93d5b606324c5dbd5b94d08c3976fc660e) Use PHP 7.1 for Postgres builds (Robbie Averill)
 * 2019-07-19 [e85f9fb](https://github.com/dnadesign/silverstripe-elemental/commit/e85f9fbd11fa0ef4c68987d76268da3a16d7081f) Use trusty distro in Travis builds (Robbie Averill)
 * 2019-07-19 [9c165a1](https://github.com/silverstripe/silverstripe-realme/commit/9c165a186128560a2d7ae7f28d99d4782992a432) Update SilverStripe versions in Travis builds (Robbie Averill)
 * 2019-07-19 [13d0cc1](https://github.com/tractorcow-farm/silverstripe-fluent/commit/13d0cc10b0c47622676b9d86e8eb085302c139c7) Update SilverStripe test versions in Travis (Robbie Averill)
 * 2019-07-19 [6040646](https://github.com/tractorcow-farm/silverstripe-fluent/commit/604064672f42e36b20aed2c9280e04fd15fd4c08) Replace filter grid with checkbox set (Ian Patel)
 * 2019-07-18 [1fb7830](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/1fb7830ff16b7ccb66f450f9057d885bb23fb341) Update core releases tested against in Travis config (Garion Herman)
 * 2019-07-17 [6c41f00](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/6c41f00c4e2ac27f9b4a9ea2999ec6d568ffbafb) Bump contentreview version in Travis (Robbie Averill)
 * 2019-07-17 [b6f8ce3](https://github.com/dnadesign/silverstripe-elemental/commit/b6f8ce3ea757961e4ad35e4b776c37b7b188bc17) Specify trusty distro in Travis builds (Robbie Averill)
 * 2019-07-17 [16fb5fd](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/16fb5fdbdb0f127cb09cedf726eb597f2040bf7c) DOCS Update namespace referenced classes in readme (Robbie Averill)
 * 2019-07-16 [2d176e2](https://github.com/tractorcow-farm/silverstripe-fluent/commit/2d176e2582e69547b0edd0cac662f769ba701f85) Add `$SelectedLanguage` template variable to fluent. Already exists in `cwp/cwp` but it should be available in `FluentExtension` (bergice)
 * 2019-07-11 [6caee34](https://github.com/bringyourownideas/silverstripe-maintenance/commit/6caee346219d55a3e2fa8ad1d324b8d76a563b2d) Bump lodash.mergewith from 4.6.1 to 4.6.2 (dependabot[bot])
 * 2019-07-09 [3cdbc9d](https://github.com/silverstripe/silverstripe-realme/commit/3cdbc9d0fe373d14c0081f59bf933db0a95e3b6d) Update phone numbers (Indy Griffiths)
 * 2019-07-07 [eec26e5](https://github.com/symbiote/silverstripe-advancedworkflow/commit/eec26e5adfce78e096afe177c6e83e23968082a4) WorkflowReminderJob missing assigned member emails (Will Rossiter)
 * 2019-07-03 [bc74040](https://github.com/silverstripe/silverstripe-tagfield/commit/bc7404005b7d2e334662f0f6b139588161e87e14) Add screenshot to readme (Ingo Schommer)
 * 2019-07-03 [461d467](https://github.com/silverstripe/silverstripe-tagfield/commit/461d467e3f8d7e21e01d74beef1fab3dd4a6305e) Added screenshot (Ingo Schommer)
 * 2019-07-03 [ec8ca5b](https://github.com/silverstripe/silverstripe-tagfield/commit/ec8ca5bf2aff6c3f7b1a85062945d4037cc48e54) DOCS Note about CMS usage (Ingo Schommer)
 * 2019-07-03 [dd18648](https://github.com/silverstripe/silverstripe-blog/commit/dd18648ed1f2941d3f3a61e3c22713ac7c91be4f) Make featured images directory configurable (Tim Burt)
 * 2019-07-02 [b3fe6d8](https://github.com/silverstripe/silverstripe-comments/commit/b3fe6d82b47e2a317df69f8b1640918689f7153a) Add legacy YAML for upgrading (Will Rossiter)
 * 2019-07-02 [cf0c2f7](https://github.com/tractorcow-farm/silverstripe-fluent/commit/cf0c2f7bcac60c80940ae1fe13673440029417c4) add .upgrade.yml (wernerkrauss)
 * 2019-07-01 [2cbbd5a](https://github.com/silverstripe/silverstripe-hybridsessions/commit/2cbbd5ae5e8ae1846296b47cf31a51fbe84434ac) Remove SilverStripe 4.0-4.2 from Travis builds (Robbie Averill)
 * 2019-06-30 [14283d8](https://github.com/silverstripe/silverstripe-blog/commit/14283d88b8d633b78e6595be441a7d2f1948552e) Set docblock for the setButtonName method, and don't invalidate localisation text. (Ryan Potter)
 * 2019-06-30 [e6a7a4c](https://github.com/silverstripe/silverstripe-blog/commit/e6a7a4c8e8ae6ec0da4b65315d0cc6453b022f36) Update SilverStripe versions in Travis builds (Robbie Averill)
 * 2019-06-30 [651d6c1](https://github.com/silverstripe/silverstripe-blog/commit/651d6c1da97b05ec81b9fcfef7a92a5c82ca15c4) Remove .idea folder from version control (Ryan Potter)
 * 2019-06-30 [ea2fcd0](https://github.com/silverstripe/silverstripe-blog/commit/ea2fcd0b6ecb4c65cdb7fb2e82d515b7c52aa7e1) Added a method to set the button name in a GridFieldAddByDBField component (Ryan Potter)
 * 2019-06-28 [bb45d27](https://github.com/silverstripe/silverstripe-restfulserver/commit/bb45d27869448c66453a64d8e0805cd20e25a32b) Update Travis build matrix (Robbie Averill)
 * 2019-06-28 [85bee89](https://github.com/silverstripe/cwp-watea-theme/commit/85bee89d4aa04059e96ce6d74f0ce823f6e20fae) Add translation to aria-label (Sacha Judd)
 * 2019-06-28 [51c4647](https://github.com/silverstripe/cwp-watea-theme/commit/51c46476ee759b369845468ad33653da92d19f18) Rebuild dist files to pull in legend size change in starter theme (Robbie Averill)
 * 2019-06-27 [098ff28](https://github.com/silverstripe/recipe-authoring-tools/commit/098ff28ebf7eddc7c88809fd247208a42145c2c3) Use trusty in Travis builds (Robbie Averill)
 * 2019-06-27 [2fb0f67](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/2fb0f678670df1387163b485e2567d9e6964bd19) Add MFA testsuite to phpunit (Robbie Averill)
 * 2019-06-27 [8f3798d](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/8f3798dc19cb04b06c72617b21ab037ab2d3884d) Update recipes and constraints for SilverStripe 4.5/CWP 2.4, add MFA dependencies and test suite, remove PHP 5.6 (Robbie Averill)
 * 2019-06-27 [d6ada01](https://github.com/silverstripe/cwp-recipe-cms/commit/d6ada01ba1ecb013826b89534f5e4f609c2c831a) Remove PHP 5.6 from Travis builds (Robbie Averill)
 * 2019-06-27 [296b755](https://github.com/silverstripe/cwp-recipe-core/commit/296b755dcc430f63b3712aa90ac447520cafce8f) Remove PHP 5.6 from Travis builds (Robbie Averill)
 * 2019-06-27 [2f2ff54](https://github.com/silverstripe/cwp-installer/commit/2f2ff54305525367da33719728866de4b42f91b6) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [5f55861](https://github.com/silverstripe/cwp/commit/5f5586199e909ed68b3501aede2939be566ad4cd) Remove PHP 5.6 from Travis builds (Robbie Averill)
 * 2019-06-27 [73f0770](https://github.com/silverstripe/recipe-authoring-tools/commit/73f0770694b5d6d295d1c16e48d537118c5baeea) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [e877cba](https://github.com/silverstripe/recipe-reporting-tools/commit/e877cba1b8356f8cfe6e53492c77566daad12321) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [5e5fce8](https://github.com/silverstripe/recipe-form-building/commit/5e5fce8259c3540e70fdf2e8747ae1f5802c6f62) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [79a66ea](https://github.com/silverstripe/recipe-content-blocks/commit/79a66eab51ed4483c9f49e7b2d02c469526be5a7) Update root version in Travis (Robbie Averill)
 * 2019-06-27 [3cac925](https://github.com/silverstripe/recipe-content-blocks/commit/3cac9255e114f6964dea372ab2c7a9e3e86a87da) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [6411f5e](https://github.com/silverstripe/recipe-collaboration/commit/6411f5e7c8ef0f682683fc65fdd9bfa742a30e37) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [1717233](https://github.com/silverstripe/recipe-blog/commit/17172334b18c78922f51e0856bbed66479fd831e) Update dependencies for SilverStripe 4.5 (Robbie Averill)
 * 2019-06-27 [223ba66](https://github.com/silverstripe/cwp/commit/223ba66fb55b5f879c9e5a57690d1a3fce433634) DOCS Update supported PHP versions (Bryn Whyman)
 * 2019-06-27 [5f0bd8e](https://github.com/silverstripe/cwp/commit/5f0bd8edcea9be79c185fb4f6c4f4e41e8e49fd8) Update supported PHP versions (Indy Griffiths)
 * 2019-06-26 [20079bd](https://github.com/silverstripe/silverstripe-textextraction/commit/20079bd33f9d28ac8352eb1f37f235c9ecc57d72) Remove SilverStripe 4.0-4.2 from Travis builds (Robbie Averill)
 * 2019-06-25 [67d10ec](https://github.com/silverstripe/silverstripe-subsites/commit/67d10ec0cb514c687c54d9c24194f5e45de7f65f) Remove SilverStripe 4.0-4.2 from Travis builds (Robbie Averill)
 * 2019-06-24 [614819a](https://github.com/silverstripe/silverstripe-subsites/commit/614819a1d373cbb13151ac4520aa8d4df16f3920) Reduce Behat builds to SS 4.3 and update postgres version (Robbie Averill)
 * 2019-06-24 [eddbc90](https://github.com/silverstripe/silverstripe-subsites/commit/eddbc905240b6f87d9416218b7df54c83d95a6a7) Remove SilverStripe 4.0-4.2 from Travis builds (Robbie Averill)
 * 2019-06-19 [994e994](https://github.com/silverstripe/cwp-core/commit/994e99415de17b47e187e4ca506bbd39560bf874) Clarify testEncrypt() uses 10000 iterations to generate its expected result (Robbie Averill)
 * 2019-06-18 [2c7a944](https://github.com/silverstripe/cwp-core/commit/2c7a944e32c02bcba7b9e1c3154391387ffafc94) DOCS Add note that changing the number of iterations in PBKDF2 would break existing hashes (Robbie Averill)
 * 2019-06-14 [40ad8d1](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/40ad8d1dacb3b2444313b6119cbf1923c2845cc6) DOCS Twig improvements to change log template (Bryn Whyman)
 * 2019-06-14 [0ac96d3](https://github.com/dnadesign/silverstripe-elemental/commit/0ac96d31a78a5544d8de6249c412ea55913f7c9b) Bump PHP memory limit (Garion Herman)
 * 2019-06-14 [829fabe](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/829fabedc74b5a8de18471f31bc4f0444fd75f9d) DOCS new headings for change log template (Bryn Whyman)
 * 2019-06-12 [b1c1931](https://github.com/silverstripe/silverstripe-subsites/commit/b1c1931d5d101c64e3a7da8b2bb0aca8414e1b0b) Detect domains correctly in Director sub-calls (Nik Rolls)
 * 2019-06-11 [7e40c59](https://github.com/silverstripe/cwp/commit/7e40c593f3792e401abd36ce67cd9309af81db97) DOCS Add changelog entry for environmentcheck's CVE-2019-12246 patch (Robbie Averill)
 * 2019-06-11 [a3f9bcc](https://github.com/silverstripe/cwp/commit/a3f9bcca8bfb1065c957630a3535388ad09a3c1b) DOCS Remove unreleased notice on CWP 2.3.0 changelog (Robbie Averill)
 * 2019-06-11 [783576c](https://github.com/silverstripe/cwp/commit/783576c716c8b3696e0a41e9d41faa7abdfe7813) DOCS 4.4.0 core release for CWP 2.3.0 (Robbie Averill)
 * 2019-06-10 [94861e5](https://github.com/silverstripe/cwp/commit/94861e5d94cf61decfe69a9872ca85ab9fc5c233) DOCS Clarify public webroot behaviour in CWP (Ingo Schommer)
 * 2019-06-09 [3ae422c](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/3ae422cd8b8b9e661adf04a9b3978e1575c60f37) Preserve and restore GridState (Fixes #31) (Will Rossiter)
 * 2019-06-06 [26b79a3](https://github.com/silverstripe/silverstripe-ldap/commit/26b79a391b2167ae3ca606ba41fe8af7279d3215) prevent undefined index error if displayname is not available (Benedikt Hofstaetter)
 * 2019-06-06 [c4c8aef](https://github.com/silverstripe/silverstripe-ldap/commit/c4c8aef91d82b1ddb7a1125092b7cc7bd339ac28) store image fields in yml configuration instead of using an extension to add them (Benedikt Hofstaetter)
 * 2019-06-05 [287e8f0](https://github.com/silverstripe/silverstripe-ldap/commit/287e8f03f515bc82c409350303dec863f6733b50) added extends to update gateway filter (Benedikt Hofstaetter)
 * 2019-06-05 [d70dccf](https://github.com/silverstripe/silverstripe-ldap/commit/d70dccf38fd4439382e1dcded2c5655058c7657d) added extend to define multiple ad fields that contain an image (Benedikt Hofstaetter)
 * 2019-06-05 [f650382](https://github.com/silverstripe/silverstripe-subsites/commit/f6503822e8bd55edeb444bf9e988308163f3ec7a) DOCS Fix typos (Robbie Averill)
 * 2019-05-31 [2b26876](https://github.com/silverstripe/silverstripe-subsites/commit/2b268765965568f929b04ee98c857a2a06678a98) Add test for URLSegment prefix set to primary subsite domain for page (Robbie Averill)
 * 2019-05-31 [900d04d](https://github.com/silverstripe/silverstripe-subsites/commit/900d04d94af650a4ee1ac65ebb40cd0f35fc0574) Add tests and move logic into the if statement (Robbie Averill)
 * 2019-05-30 [2a9f3ac](https://github.com/silverstripe/silverstripe-subsites/commit/2a9f3ac0f6bf7ef66b5e7692e1269fca14131a29) DOCS Fix phpdoc in summary_fields (Robbie Averill)
 * 2019-05-30 [2644083](https://github.com/silverstripe/silverstripe-subsites/commit/2644083a2d17b8c8f38004a68a9144a33137e587) Remove code coverage, it is segfaulting on SS 4.4 (Robbie Averill)
 * 2019-05-30 [68c763d](https://github.com/silverstripe/silverstripe-subsites/commit/68c763da3e664393b8d3bcb47b41860c6b289fe4) Tidy output of IsPublic value in Subsites admin (Garion Herman)
 * 2019-05-30 [3b8207d](https://github.com/silverstripe/silverstripe-subsites/commit/3b8207d70cb98c42f1fdf204e815a0a078fdaa5e) Ensure URL segment field type before using its API, and add docs around subsite and fluent domain compatibility (Robbie Averill)
 * 2019-05-30 [06a1658](https://github.com/dnadesign/silverstripe-elemental/commit/06a1658b31622f5a5f652f8d2d469db90ea2e3db) Renamed hooks to be more explicit (StephenMak)
 * 2019-05-30 [6fac911](https://github.com/dnadesign/silverstripe-elemental/commit/6fac911133445a6cdef40845ba8ea807df4d06fd) Added additional script to .travis.yml before_script section (StephenMak)
 * 2019-05-29 [687b85f](https://github.com/dnadesign/silverstripe-elemental/commit/687b85fd1885f0e654a515b363fac57f0f05f3dc) Add extension hooks to requireDefaultRecords (StephenMak)
 * 2019-05-28 [284aced](https://github.com/silverstripe/silverstripe-restfulserver/commit/284aceddd00db6d407a860058da14a181361efee) Use trusty in Travis builds (Robbie Averill)
 * 2019-05-28 [ea430a1](https://github.com/silverstripe/cwp/commit/ea430a1c26e8701f5e04cbf02baaf1a70d210cc1) DOCS Update release docs (Bryn Whyman)
 * 2019-05-27 [b64df9a](https://github.com/silverstripe/cwp/commit/b64df9a99a206e787357faceb39cccfd91dd5e5f) Replace fancy quotes with standard quotes (Robbie Averill)
 * 2019-05-27 [3910acf](https://github.com/silverstripe/cwp/commit/3910acf7532a8a9f8c41ea6f3e58b9f7ef7a68b0) Update 10_Security.md (JessicaSilverStripe)
 * 2019-05-17 [b1c853e](https://github.com/silverstripe/silverstripe-blog/commit/b1c853eafe4a1fbe3a4c554e581d2594c1dad1a9) UX expand custom summary if field has value (#587) (Guy Marriott)
 * 2019-05-17 [679e690](https://github.com/silverstripe/silverstripe-blog/commit/679e690ca5107c0b93b39a6805b648d04ee89ec0) UX expand custom summary if field has value (Nic Horstmeier)
 * 2019-05-17 [d141c83](https://github.com/silverstripe/silverstripe-userforms/commit/d141c83e0a1eda6686ccfca9c30d2d893c8b860a) Import missing PHPDoc doc blocks, switch intval() for (int) casting (Robbie Averill)
 * 2019-05-17 [097edbc](https://github.com/silverstripe/silverstripe-iframe/commit/097edbc9c2b6d58ac358b655fe36750fa285cff3) Update title and description of IFrameTitle field (Robbie Averill)
 * 2019-05-16 [14b35f1](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/14b35f1935c9954041fc995165d39ca82ff604a7) DOCS Fix doc block formatting in SolrService (Robbie Averill)
 * 2019-05-16 [b1ec2ed](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/b1ec2ed6d9cd35d6c5e8669ebc8d4fdb9b320558) Remove unused class imports, import docblock reference for Apache_Solr_Response, use strict comparison (Robbie Averill)
 * 2019-05-16 [617501e](https://github.com/silverstripe/silverstripe-comments/commit/617501efed8644f9726bfba23a13dbc85894fcf3) comments extension filters on Parent Class (Heath Dunlop)
 * 2019-05-15 [b44203b](https://github.com/silverstripe/silverstripe-restfulserver/commit/b44203b800e39dd828ec8d5992ccc3964e45c344) DOCS Fix formatting endpoint descriptions (Robbie Averill)
 * 2019-05-15 [6b65424](https://github.com/silverstripe/silverstripe-sharedraftcontent/commit/6b6542450a41c5d10775f0b4ea5bb638ba0971ce) Add legacy.yml for SS3 to SS4 upgrades (Sheila Bañez)
 * 2019-05-15 [7df0659](https://github.com/symbiote/silverstripe-advancedworkflow/commit/7df0659d36037a65f017c3745d0d16af8aacd49d) Add legacy.yml for SS3 to SS4 upgrades (Sheila Bañez)
 * 2019-05-15 [a1b7d39](https://github.com/silverstripe/silverstripe-externallinks/commit/a1b7d3979ef7b8d67d9f3c5cb258ea92c641f141) Add legacy.yml for SS3 to SS4 upgrades (Sheila Bañez)
 * 2019-05-12 [98183ad](https://github.com/silverstripe/silverstripe-blog/commit/98183ad6775bec92739f7956850054d3de67578f) Update references to text fixtures and SS_List class namespace from cherry-picked SilverStripe 3 commit (Robbie Averill)
 * 2019-05-09 [7e09683](https://github.com/symbiote/silverstripe-advancedworkflow/commit/7e09683211740f9925f0258a3e5a07bf358d788f) Update translations (Robbie Averill)
 * 2019-05-09 [5758075](https://github.com/silverstripe/silverstripe-userforms/commit/5758075d42dacb05dba8846d10699b22b55fb525) Update translations (Robbie Averill)
 * 2019-05-09 [ee527a4](https://github.com/silverstripe/silverstripe-sitewidecontent-report/commit/ee527a4d538d34d69b846a586f82cb6aef37127b) Update translations (Robbie Averill)
 * 2019-05-09 [8e8de7f](https://github.com/silverstripe/silverstripe-realme/commit/8e8de7f7372872081d07e9e28aac6edb73416862) Update translations (Robbie Averill)
 * 2019-05-09 [4e84936](https://github.com/silverstripe/silverstripe-ldap/commit/4e84936a7eba0cf3eaf5dcb23cda4662cd064f52) Update translations (Robbie Averill)
 * 2019-05-09 [3fcebd6](https://github.com/silverstripe/silverstripe-hybridsessions/commit/3fcebd6399d18397a59a137856d63cef9170cda7) Update translations (Robbie Averill)
 * 2019-05-09 [565a9e1](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/565a9e11e4db49eebbb90cabd32cde7a53386a5d) Update translations (Robbie Averill)
 * 2019-05-09 [1ab3e24](https://github.com/silverstripe/silverstripe-elemental-bannerblock/commit/1ab3e24e584aeb97b109811b5bde02d33cc8fb5b) Update translations (Robbie Averill)
 * 2019-05-09 [ec11687](https://github.com/silverstripe/silverstripe-blog/commit/ec116870f50a4e86fd5033382fffc4ca26d48d51) Update translations (Robbie Averill)
 * 2019-05-09 [33af9b7](https://github.com/dnadesign/silverstripe-elemental/commit/33af9b78cdcf576fab7a71cda8dac007f3b62494) Update translations (Robbie Averill)
 * 2019-05-09 [55116fb](https://github.com/silverstripe/cwp-search/commit/55116fbdb9ec703e7a36c358dcafd9978d0b98ab) Update translations (Robbie Averill)
 * 2019-05-09 [23febb8](https://github.com/silverstripe/cwp-agencyextensions/commit/23febb8e1a560bedf895e9741844629bab627bbe) Update translations (Robbie Averill)
 * 2019-05-09 [22e2a8d](https://github.com/bringyourownideas/silverstripe-maintenance/commit/22e2a8d671c9062fc693dfc60173d37872cab1de) Update translations (Robbie Averill)
 * 2019-05-09 [4d016e0](https://github.com/tractorcow-farm/silverstripe-fluent/commit/4d016e0114f649ed7825116b23104669feb1b046) Add PHP 7.3 and SilverStripe 4.3/4.4 to Travis builds (Robbie Averill)
 * 2019-05-09 [997a1a9](https://github.com/tractorcow-farm/silverstripe-fluent/commit/997a1a92dd4aa993348d1c62e1af7c96dc344d20) Update translations (Robbie Averill)
 * 2019-05-03 [441b73c](https://github.com/dnadesign/silverstripe-elemental/commit/441b73c37444f6ed8b57e7b3bae93aaee85453ab) DOCS Fix broken userhelp reference to userforms module (Robbie Averill)
 * 2019-05-02 [f3fc1fa](https://github.com/silverstripe/cwp-search/commit/f3fc1fa58abf58c84f3ec85bf4bc4a45d003aafe) Use database in functional test (Robbie Averill)
 * 2019-04-29 [3a9ac5e](https://github.com/dnadesign/silverstripe-elemental/commit/3a9ac5e44edd3e67a3eefa911a52fda5b32ff4e0) DOCS Comment docs updates to new migration task (Robbie Averill)
 * 2019-04-29 [6276ad2](https://github.com/silverstripe/silverstripe-tagfield/commit/6276ad2aee12a643474c4d6c91335960449509aa) php cs fixes (Nivanka Fonseka)
 * 2019-04-17 [73339bf](https://github.com/tractorcow-farm/silverstripe-fluent/commit/73339bf05c12f377995e4af409d873b44d4819f9) Use the locale's URLSegment as default badge label (JorisDebonnet)
 * 2019-04-17 [fece48c](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/fece48c5f03c3a1b9faea4d4e54bcdb4fe0253a4) DOCS Fix broken phpdoc types and tighten string comparison operators (Robbie Averill)
 * 2019-04-15 [a5da7df](https://github.com/silverstripe/silverstripe-gridfieldqueuedexport/commit/a5da7dfe7679e04e2a0311f8f15d3e8b2a73a625) Update Travis matrix to include SS ^4.2 and PHP 7.3 (Robbie Averill)
 * 2019-04-15 [d1f7394](https://github.com/silverstripe/cwp-recipe-kitchen-sink/commit/d1f73949eb31724009f0bd4cb884eb810567658f) Move silverstripe/mfa and silverstripe/totp-authenticator into Travis only builds (Robbie Averill)
 * 2019-04-11 [c490c4e](https://github.com/silverstripe/silverstripe-environmentcheck/commit/c490c4e5a570635a3227dc04691d3da35813b89b) ADD ConfirmationMiddleware exceptions for the dev routes (Serge Latyntcev)
 * 2019-04-05 [2c94814](https://github.com/tractorcow-farm/silverstripe-fluent/commit/2c948144e65644bfd77dce939b5d396d7514a34d) Clearer Versioned example (Ingo Schommer)
 * 2019-03-28 [22bb37f](https://github.com/silverstripe/recipe-authoring-tools/commit/22bb37f6a8deef7bfe03b00b9aa0aabf3084705d) Update dependancy constraints (Will Rossiter)
 * 2019-02-13 [c134ce4](https://github.com/silverstripe/silverstripe-blog/commit/c134ce44c1b9b10c52ebaeae9f74729362506141) Switch assertions to test the end of the strings (Robbie Averill)
 * 2019-02-04 [ac404c9](https://github.com/silverstripe/silverstripe-hybridsessions/commit/ac404c92a64c050dfd3cb5a9055dc356b429e26b) Implemented variables for multiple use (Andreas Gerhards)
 * 2019-02-04 [59e1476](https://github.com/silverstripe/silverstripe-hybridsessions/commit/59e147667ed155df19e3c0c4832184418d474a8f) Added comment to explain the cookie deletion (gelysis)
 * 2019-02-01 [a91425f](https://github.com/silverstripe/silverstripe-hybridsessions/commit/a91425f7c443419665d1896ec8253debaab69bb7) Corrected indentation (gelysis)
 * 2019-02-01 [3512588](https://github.com/silverstripe/silverstripe-hybridsessions/commit/35125889f9e91d85e31abd7d44d6662934a34992) Removed outdated cookie as well (gelysis)
 * 2019-02-01 [f273079](https://github.com/silverstripe/silverstripe-hybridsessions/commit/f2730795acd8e215719cb7e17d1d0c33245344ec) Replaced unset with null assignment (gelysis)
 * 2019-02-01 [18c31a0](https://github.com/silverstripe/silverstripe-hybridsessions/commit/18c31a00c924378c72d88b3077ec9ea54e436e71) Added data unset to stop data being read from outdated cookie (gelysis)
 * 2019-01-10 [5a5c3b0](https://github.com/silverstripe/silverstripe-hybridsessions/commit/5a5c3b085eb9397954345d9b86dda362ba6fe9a0) Add PHP 7.3 and SilverStripe 4.3 to Travis builds, and use recipe-cms to fix versioned mismatch (Robbie Averill)
 * 2018-12-17 [94dd537](https://github.com/silverstripe/silverstripe-hybridsessions/commit/94dd537fbf50ff591a0d2decab3b48489c04d80a) DOCS Update readme to indicate CryptoHandler options and point out that mcrypt is deprecated (Robbie Averill)
 * 2018-12-03 [63e4252](https://github.com/tractorcow-farm/silverstripe-fluent/commit/63e425248f66b79b71212533081cad2bc32b4a9c) move opening brace to a new line (AljosaB)
 * 2018-12-03 [e91e86a](https://github.com/tractorcow-farm/silverstripe-fluent/commit/e91e86abaa38b80012509831838de15168497ef9) add alternate links to metatags (Aljoša Balažic)
 * 2018-11-08 [13dc1dc](https://github.com/silverstripe/silverstripe-hybridsessions/commit/13dc1dcb6e689830943340dc6b788ec969900de0) Revert "Only initialise session if HybridSession is enabled" (Guy Marriott)
 * 2018-11-07 [7de2a23](https://github.com/tractorcow-farm/silverstripe-fluent/commit/7de2a23f9014106744df7a4dbd452cd33c139e9c) Bump alias for master to 4.3.x-dev (Robbie Averill)
 * 2018-10-10 [068e4c6](https://github.com/silverstripe/silverstripe-tagfield/commit/068e4c6a268dddf2018fde62a53f42dbbe256742) Setup TagField to work within AssetAdmin (Fixes #107) (Will Rossiter)
 * 2018-07-06 [3d9031a](https://github.com/silverstripe/silverstripe-blog/commit/3d9031aaacc19312628141c6303446361a7bd981) Adding ansi quote to identifier (3Dgoo)
 * 2018-06-29 [3177296](https://github.com/silverstripe/silverstripe-blog/commit/317729604dd52bd90085ba3db16a7341b660a09b) Adding tests (3Dgoo)
 * 2018-06-17 [c8ddec1](https://github.com/silverstripe/silverstripe-restfulserver/commit/c8ddec1ecb1857a5a50c0f596fb9aeae1c3f4288) Add supported module badge to readme (#71) (Dylan Wagstaff)
 * 2018-06-15 [67acd83](https://github.com/silverstripe/recipe-authoring-tools/commit/67acd83a231a5e27afd78b3bc535acbf1f0ae7e2) Add supported module badge to readme (Dylan Wagstaff)
 * 2018-06-15 [a94652d](https://github.com/silverstripe/silverstripe-auditor/commit/a94652d3c8adafc38db94c00048616e9683b7c50) Add supported module badge to readme (Dylan Wagstaff)
<!--- Changes above this line will be automatically regenerated -->
