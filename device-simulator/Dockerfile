FROM node:14.15.2

# 컨테이너 안에서 작업할 디렉터리 지정
WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 8369

CMD ["node", "app.js"]
