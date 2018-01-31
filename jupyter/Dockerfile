FROM jupyter/datascience-notebook

RUN python --version

RUN conda install --quiet --yes -c \
    conda-forge osmnx dask

USER root

RUN conda update -y --all

RUN apt-get update && apt-get install -y \
      libsqlite3-dev \
      zlib1g-dev \
      python-pydot \
      python-pydot-ng \
      graphviz \
      cmake \
      libtool \
      && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/mapbox/tippecanoe.git \
      && cd tippecanoe && make all && make install

RUN git clone https://github.com/uber/h3.git \
      && cd h3 && cmake . && make && make install

RUN pip install -U geopandas \
                   geopy \
                   rtree \
                   folium \
                   numpy \
                   shapely \
                   fiona \
                   six \
                   pyproj \
                   numexpr==2.6.4 \
                   elasticsearch \
                   geojson \
                   plotly \
                   tqdm \
                   mapbox \
                   mapboxgl \
                   cufflinks \
                   python-geohash \
                   tables \
                   mixpanel \
                   SQLAlchemy \
                   GeoAlchemy2 \
                   mapbox-vector-tile \
                   xgboost \
                   jupyter_contrib_nbextensions \
                   jupyter_nbextensions_configurator \
                   palettable \
                   graphviz

USER $NB_USER

RUN jupyter contrib nbextension install --user
RUN jupyter nbextensions_configurator enable --user

ADD fonts /usr/share/fonts/truetype/

RUN fc-cache
RUN fc-list

VOLUME /notebooks
WORKDIR /notebooks
