# 🎯 Targetting Specific Keycloak Versions

By default, Keycloakify generates multiples jar files, each one meant to be used with a given Keycloak version range.

<figure><img src=".gitbook/assets/image (21).png" alt="" width="315"><figcaption><p>files generated by 'keycloakify build' when you have a Multi Page Account theme</p></figcaption></figure>

However you might want to customize this behavior. If you know ahead of time what Keycloak you theme will using you can build only for this version using the `keycloakVersionTargets` build option.

{% tabs %}
{% tab title="Vite" %}
<pre class="language-typescript" data-title="vite.config.ts"><code class="lang-typescript">import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import { keycloakify } from "keycloakify/vite-plugin";

// https://vitejs.dev/config/
export default defineConfig({
    plugins: [react(), keycloakify({
        accountThemeImplementation: "none", 
<strong>        keycloakVersionTargets: {
</strong><strong>            "21-and-below": false,
</strong><strong>            "22-and-above": "my-keycloak-theme.jar"
</strong><strong>        }
</strong>    })]
});
</code></pre>
{% endtab %}

{% tab title="Webpack" %}
<pre class="language-json" data-title="package.json"><code class="lang-json">{
    "keycloakify": {
        "accountThemeImplementation": "none", 
<strong>        "keycloakVersionTargets": {
</strong><strong>            "21-and-below": false,
</strong><strong>            "22-and-above": "my-keycloak-theme.jar"
</strong><strong>        }
</strong>    }
}
</code></pre>
{% endtab %}
{% endtabs %}

In this configuration only the  jar for Keycloak 22 and above will be generated by `npx keycloakify build`. and the file will be: dist\_keycloak/my-keycloak-theme.jar.

{% hint style="info" %}
If you have [a Multi Page account theme](keycloak-configuration/enabling-your-theme/account-theme.md) the keycloakVersionTargets expected changes! Use TypeScript auto completion to know what ranges are required to be filled.&#x20;
{% endhint %}