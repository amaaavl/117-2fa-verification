<?php
header('Content-Type: application/json');

// SECURE API KEY
define('API_KEY', '12345678'); // change this to something secret

// Encrypted domain list (base64 encoded for extra security)
$encryptedDomains = [
    base64_encode('domain.com'),
    base64_encode('test.com'),
    base64_encode('yourwebsite.ng'),
];

// Receive data
$receivedKey = $_GET['key'] ?? $_POST['key'] ?? '';
$receivedDomain = $_GET['domain'] ?? $_POST['domain'] ?? '';

// Normalize and secure domain
$receivedDomain = strtolower(trim($receivedDomain));

// Anti-null check
if ($receivedKey !== API_KEY) {
    echo json_encode([
        'status' => 'unauthorized',
        'message' => 'Invalid API Key'
    ]);
    exit;
}

if (empty($receivedDomain)) {
    echo json_encode([
        'status' => 'error',
        'message' => 'No domain provided.'
    ]);
    exit;
}

// Check if domain matches encrypted list
$found = false;
foreach ($encryptedDomains as $encDomain) {
    if (base64_decode($encDomain) === $receivedDomain) {
        $found = true;
        break;
    }
}

if ($found) {
    echo json_encode([
        'status' => 'valid',
        'message' => 'License is valid for this domain.',
        'domain' => $receivedDomain
    ]);
} else {
    echo json_encode([
        'status' => 'invalid',
        'message' => 'Domain is not licensed.',
        'domain' => $receivedDomain
    ]);
}
exit;
?>
