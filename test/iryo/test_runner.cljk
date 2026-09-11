(ns iryo.test-runner (:require [clojure.java.io :as io] [clojure.test :as test]))
(defn suites [] (->> (file-seq (io/file "test")) (filter #(and (.isFile %) (re-matches #".*test.*\.clj[cs]?" (.getName %)))) (keep #(some-> (re-find #"\(ns\s+([^\s\)]+)" (slurp %)) second symbol)) (remove #{'iryo.test-runner}) distinct sort vec))
(defn -main [& _] (let [xs (suites)] (doseq [x xs] (require x)) (let [{:keys [fail error]} (apply test/run-tests xs)] (shutdown-agents) (System/exit (if (zero? (+ fail error)) 0 1)))))
