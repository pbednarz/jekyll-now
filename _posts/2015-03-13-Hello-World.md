---
published: true
---

## A New Post

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.
![](/http://services.google.com/fh/files/misc/android-developers-logo.png)

Fetching and saving API data using Retrifit Observable (RxJava) and OrmLite:
```java
private void loadAlbum() {
    refreshLayout.setRefreshing(true);
    retrofitSubscription = AppObservable.bindFragment(this, Service.getInstance(getActivity())
            .getNewClientInstance().getAlbum(getArguments().getString(ALBUM_NAME_KEY))
            .doOnNext(album -> DatabaseManager.getInstance(getActivity().getApplicationContext())
                    .saveAlbum(album))
            .subscribeOn(Schedulers.io()))
            .subscribe(album -> {
                        mAdapter.setAlbum(album);
                        mAdapter.notifyDataSetChanged();
                    },
                    exception -> {
                        exception.printStackTrace();
                        refreshLayout.setRefreshing(false);
                    }, () -> refreshLayout.setRefreshing(false));
}
```