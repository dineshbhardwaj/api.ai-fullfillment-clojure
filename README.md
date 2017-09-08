# api.ai-fullfillment-clojure
api.ai works with clojure and heroku flowlessly
Here are the steps to make your Clojure code work with Heroku. 
Following is the assumption : lein is already working with clojure at your end. 
use the following link to creat a heroku account and use there closure supported web engine to generate a site for you.

https://devcenter.heroku.com/articles/getting-started-with-clojure#introduction

read/understand at least : 
https://devcenter.heroku.com/articles/getting-started-with-clojure#push-local-changes

after that you can replace the project.clj and web.clj with the present above and you will be able to process the input json query with the answer as the same output which is input.  

Following is the code used in above files : 

(defn handler 
  ;;   "generating different response depending on input is posible by changing 'input_data' after json extraction"
  [request]
  (def input_data  (str  (get  (get-in (json-body-request request {:keywords? true :bigdecimals true}) [:body :result])  :resolvedQuery)))
  (response {:speech input_data
             :displayText "Turst me user, It works !!"})
  )


(def app
  (wrap-json-response handler)
  )


