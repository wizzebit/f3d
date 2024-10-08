
.. _program_listing_file_public_loader.h:

Program Listing for File loader.h
=================================

|exhale_lsh| :ref:`Return to documentation for file <file_public_loader.h>` (``public/loader.h``)

.. |exhale_lsh| unicode:: U+021B0 .. UPWARDS ARROW WITH TIP LEFTWARDS

.. code-block:: cpp

   #ifndef f3d_loader_h
   #define f3d_loader_h
   
   #include "exception.h"
   #include "export.h"
   #include "types.h"
   
   #include <filesystem>
   #include <string>
   #include <vector>
   
   namespace f3d
   {
   class F3D_EXPORT loader
   {
   public:
     struct load_failure_exception : public exception
     {
       explicit load_failure_exception(const std::string& what = "")
         : exception(what){};
     };
   
   
     virtual loader& add(const std::filesystem::path& filePath) = 0;
     virtual loader& add(const std::vector<std::filesystem::path>& filePath) = 0;
     virtual loader& add(const std::vector<std::string>& filePathStrings) = 0;
   
     virtual loader& add(const mesh_t& mesh) = 0;
   
   
     loader& add(std::initializer_list<std::string> list)
     {
       return this->add(std::vector<std::string>(list));
     }
     loader& add(std::initializer_list<std::filesystem::path> list)
     {
       return this->add(std::vector<std::filesystem::path>(list));
     }
   
     virtual loader& clear() = 0;
   
     virtual bool supports(const std::filesystem::path& filePath) = 0;
   
   protected:
     loader() = default;
     virtual ~loader() = default;
     loader(const loader& opt) = delete;
     loader(loader&& opt) = delete;
     loader& operator=(const loader& opt) = delete;
     loader& operator=(loader&& opt) = delete;
   };
   }
   
   #endif
