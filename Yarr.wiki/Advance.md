Temporary Memo

### mongoui
It is a kind of mongo gui to view data in JSON document. It allows to add, edit, delete documents.

Requires Node.js
```
sudo yum install epel-release
sudo yum install nodejs
```
then, download mongoui
```
git clone https://github.com/azat-co/mongoui.git
cd mongoui
git checkout v4.2.1
npm i
npm i opn
```

To start, type `node .` or `npm start`

It will open http://localhost:3001 automatically