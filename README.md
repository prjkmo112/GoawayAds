# How to remove ads from browser

1. open your browser's console

2. write down this code.
```javascript
function xpaths(path, parent) {
    let result = [];
    let query = document.evaluate(path, parent||document, null, XPathResult.ORDERED_NODE_SNAPSHOT_TYPE, null);

    for (let i=0; i<query.snapshotLength; i++) {
        result.push(query.snapshotItem(i));
    }

    return result;
}

setInterval(() => {
    let els = [];
    els = els.concat(xpaths(`//*[contains(@id, 'google_ads_iframe')]`));
    els = els.concat(xpaths(`//*[contains(@class, 'adsbygoogle')]`));
    for (let i in els) {
        if (!!els && !!els[i] && !!els[i].setAttribute && els[i].getAttribute('style').indexOf('display: none') < 0) {
            els[i].setAttribute('style', 'display: none;');
            console.log('delete google ads')
        }
    }

    let el = document.querySelector(`div[id*='ScriptRootC']`)
    if (!!el && !!el.shadowRoot) {
        el = document.querySelector(`div[id*='ScriptRootC']`).shadowRoot.querySelector('div')
        if (!!el && !!el && !!el.setAttribute && el.getAttribute('style').indexOf('display: none') < 0) {
            el.setAttribute('style', 'display:none;')
        }
    }
}, 100)
```