FROM overview/overview-base

RUN apt-get update

RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:alex-p/tesseract-ocr

RUN apt-get install -y \
  libreoffice \
  tesseract-ocr \
  tesseract-ocr-ara \
  tesseract-ocr-cat \
  tesseract-ocr-deu \
  tesseract-ocr-fra \
  tesseract-ocr-ita \
  tesseract-ocr-nld \
  tesseract-ocr-nor \
  tesseract-ocr-por \
  tesseract-ocr-rus \
  tesseract-ocr-spa \
  tesseract-ocr-swe 

RUN \
  export FILENAMES="$(unzip -qq -p production.zip archive/worker/classpath.txt | \
    sed -e 's/^/archive\/lib\//')" && \
  unzip -qq -d bin -j production.zip $FILENAMES && \
  rm production.zip

WORKDIR /opt/overview

CMD ["/usr/bin/java", \
       "-cp", "bin/*", \
        "-Dfile.encoding=UTF8", \
        "-Duser.timezone=UTC", \
        "com.overviewdocs.Worker"]
