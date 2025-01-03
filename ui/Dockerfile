FROM node:22 as builder

WORKDIR /app
COPY package.json /app
COPY yarn.lock /app
RUN yarn config set "strict-ssl" false && yarn install
# rm -f yarn.lock && \
#     yarn config set registry https://registry.npmjs.org/ && \
#     yarn install --force
ADD . /app
RUN  yarn build

FROM nginx:latest
COPY --from=builder /app/dist /usr/share/nginx/html
COPY --from=builder /app/default.conf /etc/nginx/conf.d/default.conf
