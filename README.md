Servidor para streaming con node
Se usa la biblioteca 
npm install node-media-server
la configuración es :
const config = {
  rtmp: {
    port: 1935,
    chunk_size: 60000,
    gop_cache: true,
    ping: 30,
    ping_timeout: 60
  },
  http: {
    port: 8000,
    mediaroot: './media',
    allow_origin: '*'
  },
  trans: {
    ffmpeg: 'C:/Users/3006080/Desktop/streaming/ffmpeg-6.0-full_build/bin/ffmpeg.exe',// se debe bajar y poner en la carpeta local el ffmep.exe, ir a la web->dar boton descargar-> elegir windows->gyan-dev->buscar releasebuils y descargar ffmpeg-release-full.7z // descomprimir en la carpeta raiz del proyecto
    tasks: [
      {
        app: 'live',// nombre para el obs, en el obs se deberá poner en conexión http://localhost/live
        hls: true,
        hlsFlags: '[hls_time=2:hls_list_size=3:hls_flags=delete_segments]',
        hlsKeep: true, // to prevent hls file delete after end the stream
        dash: true,
        dashFlags: '[f=dash:window_size=3:extra_window_size=5]',
        dashKeep: true // to prevent dash file delete after end the stream
      }
    ]
  }
};
