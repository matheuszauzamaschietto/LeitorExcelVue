<template>
    <div class="home">
        <div class="d-flex justify-content-center align-items-center home-div-base">
            <div class="col-xxl-4 col-lg-6 col-md-8 col-11">
                <div class="p-4 rounded-3 login-form-div d-flex flex-column ">
                    <h2 class="fs-4">Validar Mapeamento</h2>
                    <form action="">
                        <div class="m-4">
                            <label for="formFile" class="form-label">Selecione o mapeamento</label>
                            <input class="form-control" type="file" id="formFile" accept=".xls, .xlsx">
                        </div>
                        <button type="button" class="btn btn-success col-md-6 col-11" :disabled="loanding" @click="enviarArquivo(this)">
                            <div v-show="!loanding">
                                Enviar arquivo
                            </div>
                            <div v-show="loanding">
                                <span class="spinner-border  spinner-border-sm me-3"></span>
                                <span role="status">Carregando...</span>
                            </div>
                        </button>
                    </form>
                    <a href="" class="mt-5 link" v-show="fileDownload" id="download-link">Baixar arquivo</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
//  import excelApi from '@/repository/excelApi';

export default {
    name: 'HomeView',
    data(){
        return {
            fileDownload: false,
            loanding: false
        }
    },
    methods: {
        async enviarArquivo(){
            const fileInput = document.getElementById('formFile');

            if (fileInput.files.length > 0) {
                this.loanding = true
                this.fileDownload = false
                let formData = new FormData();
                formData.append("formFile", fileInput.files[0]);

                fetch("https://localhost:44343/excel/upload", {
                    method: 'POST',
                    body: formData
                })
                .then(response => {
                    if (!response.ok) {
                    throw new Error('Erro na requisição da API');
                    }
                    return response.blob();
                })
                .then(blob => {
                    var link = document.querySelector('#download-link');
                    link.href = window.URL.createObjectURL(blob);
                    link.download = "Mapeamento Validado.xlsx";
                    this.fileDownload = true
                })
                .catch(error => console.error('Erro:', error));

                this.loanding = false
            } else {
                alert('Nenhum arquivo selecionado.');

            }
        }
    }
}
</script>

<style scoped>
label,
h2 {
    color: var(--primaria);
}

label {
    font-size: 18px;
}

.home-div-base {
    background-color: var(--primaria);
    min-height: 100vh;
}

.login-form-div {
    background-color: rgba(255, 255, 255, 0.783);
    box-shadow: #FFFFFF 0px 0px 25px 0px;
}
</style>
