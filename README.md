# shopify-api-collections
The <strong>REST Admin API</strong> lets you build apps and other integrations for the Shopify admin.\nIf you want to create Shopify-powered storefronts for platforms outside of the Shopify admin, including websites,\nmobile apps, and game development engines, then see the\n<a href=\"https://help.shopify.com/api/storefront-api\">Storefront API</a> instead.</p><hr><p>The documentation provided as part of this Postman collection is for convenience and does not include\ncomplete, up-to-date information about the REST Admin API. For the complete documentation,\nsee <a href="https://help.shopify.com/api/reference">https://help.shopify.com/api/reference</a>.</p>

# Basic Steps
1) Create store
2) Create App in the stores
3) Copy API Key, API Secret, Access Token
4) Click on notification
5) Select shopify event and add webhook URL


# To get shopify Reponse in Webhook URL in php
define('CLIENT_SECRET', '709edeb8d0cc81ca976dba7d55063591');
function verify_webhook($data, $hmac_header)
{
    $calculated_hmac = base64_encode(hash_hmac('sha256', $data, CLIENT_SECRET, true));
    return hash_equals($hmac_header, $calculated_hmac);
}
$hmac_header = $_SERVER['HTTP_X_SHOPIFY_HMAC_SHA256'];
$data = file_get_contents('php://input');
$verified = verify_webhook($data, $hmac_header);
error_log('Webhook verified: ' . var_export($verified, true)); // Check error.log to see the result
$res = $data;
// if ($verified) {
//     $res = $data;
// } else {
//     $res = 'there maybe something wrong..';
// }
$log = fopen('product.json', 'w') or die('cant open the file');

fwrite($log, $res);
fclose($log);
