# 7G-firewall
more efficient whitelisting

<p>A whitelisting sample from https://gridpane.com/kb/using-the-7g-web-application-firewall/</p>
<p>We can exclude these two results by targeting “page=seopress-google-analytics&code” and adding an exclusion for both errors like so:</p>
<pre>
<code>
set $exclusion_rule_match "";
if ( $args ~* ^page=seopress-google-analytics&code ) {
set $exclusion_rule_match 15;
}
if ($bad_request_7g = $exclusion_rule_match) {
set $7g_drop_bad_request 0;
}

set $exclusion_rule_match "";
if ( $args ~* ^page=seopress-google-analytics&code ) {
set $exclusion_rule_match 12;
}
if ($bad_querystring_7g = $exclusion_rule_match) {
set $7g_drop_bad_query_string 0;
}
</code>
</pre>

<p>The above sample contains <b>4</b> <code>if</code> directive but Nginx <code>if</code> is evil and shouldn't be overused.</p>
