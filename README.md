# license-bypass-script-
this script lets u bypass the license verification for https://wardencode.base44.app/ you just need to put the code in dev console and then put what do u want in the license textbox and press unlock acces and boom ur in 
code:// patch crypto hashing and string comparison to force license verification match
(function() {
    const originalDigest = crypto.subtle.digest;
    crypto.subtle.digest = async function(algorithm, data) {
        let result = await originalDigest.apply(this, arguments);
        console.log('[+] Intercepted crypto hash calculation. Forcing match hash.');
        // return the exact hash of one of the valid records to trick the comparison
        // matching: c193f93b0d60b48175374ec242e3b3c7b7be284f1cbc31bd4b6934ff27143661
        let targetHex = "c193f93b0d60b48175374ec242e3b3c7b7be284f1cbc31bd4b6934ff27143661";
        let bytes = new Uint8Array(targetHex.match(/.{1,2}/g).map(byte => parseInt(byte, 16)));
        return bytes.buffer;
    };
    console.log('[+] Crypto hash spoofing active. Type any key and unlock.');
})();
