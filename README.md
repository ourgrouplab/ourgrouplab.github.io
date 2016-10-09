### View git log

git log --pretty=format:"%H %at %s"

### Convert epoch time to human time based on client in JS

```
var utcSeconds = 1234567890;
var d = new Date(0); // The 0 there is the key, which sets the date to the epoch
d.setUTCSeconds(utcSeconds);
```

### Initialize repo based on beautiful jekyll

```
REPO_NAME="aaa"

curl -u "ourgrouplab:$GITHUB_PAT" https://api.github.com/user/repos -d '{"name":"'"$REPO_NAME"'"}'

cd ~/ourgrouplab && \
git clone git@github.com:ourgrouplab/$REPO_NAME.git && \
cd $REPO_NAME && \
git checkout --orphan gh-pages && \
cp -r ~/ourgrouplab/beautiful-jekyll/* . && \
git add -A && \
git commit -m "Initial commit" && \
echo -e "url: \"http://ourgrouplab.github.io/$REPO_NAME\"\nbaseurl: \"/$REPO_NAME\"" >> _config.yml &&
git add _config.yml && \
git commit -m "Set initial default settings" && \
git push origin gh-pages
```

### Delete repo

```
curl -i -u "ourgrouplab:$GITHUB_PAT" https://api.github.com/repos/ourgrouplab/"$REPO_NAME" -X DELETE && \
rm -rf ~/ourgrouplab/$REPO_NAME 
```

Maybe move the folder to some other "trash" folder instead of removing it entirely
