<template>
    <div><br>
        <hr><br><br>
        <v-btn color="warning" @click="getImage()">Upload Files</v-btn>
    </div>
</template>

<script>
export default {
    data() {
        return {
            cameraOptions: {
                quality: 100,
                destinationType: navigator.camera.DestinationType.FILE_URI,
                sourceType: navigator.camera.PictureSourceType.PHOTOLIBRARY
            }  
        }
    },
    mounted() {
        document.addEventListener("deviceready", onDeviceReady , false);
        function onDeviceReady() {
            console.log(window.FileTransfer);
        }
    },
    methods: {
        // selectFiles() {
        //     fileChooser.open(() => {
        //         alert(`selected successfully..`)
        //     })
        // },
        getImage() {
            navigator.camera.getPicture(this.uploadPhoto, this.onError, this.cameraOptions);
        },
        onError(err) {
            alert(err);
        },
        uploadPhoto(imageURI) {
            var options = new window.FileUploadOptions();
            options.fileKey = "file";
            options.fileName = imageURI.substr(imageURI.lastIndexOf('/') + 1);
            options.mimeType = "image/jpg";
            var ft = new window.FileTransfer();
            ft.upload(imageURI, "http://localhost:5000/api/photo",
                function(result) {
                    console.log(JSON.stringify(result));
                },
                function(error) {
                    console.log(JSON.stringify(error));
            }, options);
        }
    }
}
</script> 