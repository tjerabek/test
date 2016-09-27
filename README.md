# test

```
app.get('/save', ensureAuthenticated, (req, res) => {
    const sess = req.session;
    const website = sess.selectedProject;

    Website.findById(website.id)
        .then((website) => {
            req.user.hasWebsite(website)
                .then(() => {
                    const site = website.bucket;

                    storage.uploadData({ Body: '<h1>Hello World!</h1>', ContentType: 'text/html', Key: 'index.html' }, storageConfig(site))
                        .then(() => {
                            return res.render('save', { title: website.title, url: website.baseUrl });
                        }).catch(function (err) {
                            console.log(err);
                            return res.render('save-error', { error: err });
                        });
                });
        });
});
```
